### 要求

## ![image-20250917193819025](C:\Users\57108\AppData\Roaming\Typora\typora-user-images\image-20250917193819025.png)

### 创建工作台

- ascend A2 B4
- Container image
- CPU
- Group ID
- Home disk size
- Home path
- Memory
- Non root
- NPU
- Shared path
- shm
- User ID

### 安装CANN

##### 1. 创建和激活虚拟环境

```bash
# 刷新APT软件包源列表，获取最新的软件包信息
sudo apt update

# 提供add-apt-repository命令
sudo apt install software-properties-common

# 添加deadsnakes团队的PPA源，该源提供多个Python版本
# 允许安装非默认版本的Python（如Python 3.11）
sudo add-apt-repository ppa:deadsnakes/ppa

# 从添加的PPA源安装Python 3.11
# 系统默认可能只提供较旧的Python版本，此步骤获取更新的版本
sudo apt install python3.11

# 使用Python 3.11创建名为vllm-ascend-env的虚拟环境
# 虚拟环境隔离项目依赖，避免与系统Python包冲突
python3.11 -m venv vllm-ascend-env

# 激活刚创建的虚拟环境，关闭虚拟环境用deactivate
# 后续的Python和pip命令将在该环境中运行
source vllm-ascend-env/bin/activate
```



##### 2. 安装Python基础包

```bash
# 使用清华镜像源加速下载
# 安装AI开发基础依赖包
# 'numpy<2.0.0'：指定numpy版本，避免与昇腾软件栈的兼容性问题
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple attrs 'numpy<2.0.0' decorator sympy cffi pyyaml pathlib2 psutil protobuf scipy requests absl-py wheel typing_extensions
```



##### 3. 下载和安装CANN工具包

```bash
# CANN：Compute Architecture for Neural Networks，华为昇腾处理器软件栈
# 添加Referer头绕过下载限制
# $(uname -i)：自动检测系统架构（x86_64或aarch64）
# x86_64：Intel/AMD CPU服务器；aarch64：ARM架构服务器（如华为泰山服务器）
wget --header="Referer: h#ttps://www.hiascend.com/" https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/CANN/CANN%208.2.RC1/Ascend-cann-toolkit_8.2.RC1_linux-"$(uname -i)".run

# chmod +x ...：赋予下载的安装文件可执行权限
chmod +x ./Ascend-cann-toolkit_8.2.RC1_linux-"$(uname -i)".run

# --full：完整安装模式
./Ascend-cann-toolkit_8.2.RC1_linux-"$(uname -i)".run --full
```



##### 4. 配置环境变量并安装其他 CANN 组件

```bash
# 执行 CANN 工具包安装后生成的环境变量脚本。这会配置如 PATH 和 LD_LIBRARY_PATH 等变量，以便系统能够找到 CANN 相关的库和可执行文件
source Ascend/ascend-toolkit/set_env.sh

# 针对 Ascend 910B NPU 的算子库（kernel）。它包含经过优化的底层计算函数，以加速神经网络的计算，脚本下载并安装了这个核心组件
wget --header="Referer: https://www.hiascend.com/" https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/CANN/CANN%208.2.RC1/Ascend-cann-kernels-910b_8.2.RC1_linux-"$(uname -i)".run
chmod +x ./Ascend-cann-kernels-910b_8.2.RC1_linux-"$(uname -i)".run
./Ascend-cann-kernels-910b_8.2.RC1_linux-"$(uname -i)".run --install

# NNAL：Neural Network Acceleration Library
# 提供高性能神经网络算子库
wget --header="Referer: https://www.hiascend.com/" https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/CANN/CANN%208.2.RC1/Ascend-cann-nnal_8.2.RC1_linux-"$(uname -i)".run
chmod +x ./Ascend-cann-nnal_8.2.RC1_linux-"$(uname -i)".run
./Ascend-cann-nnal_8.2.RC1_linux-"$(uname -i)".run --install

# ATB：Ascend Tensor Boost，昇腾张量加速库
# 加载ATB相关环境变量
source Ascend/nnal/atb/set_env.sh
```



### 安装vllm、vllm-ascend

##### 1. 安装系统依赖并配置 pip 镜像

```bash
# 将Ubuntu官方软件源apt替换为清华镜像源，大幅提升软件下载速度，特别是在中国境内
sed -i 's|ports.ubuntu.com|mirrors.tuna.tsinghua.edu.cn|g' /etc/apt/sources.list

# 更新软件包列表（-y自动确认）
# 安装的开发工具：
# gcc：GNU C编译器			g++：GNU C++编译器
# cmake：跨平台构建系统		 libnuma-dev：NUMA（非统一内存访问）开发库
# wget：命令行下载工具		 git：版本控制系统
# curl：数据传输工具		  jq：JSON处理工具
apt-get update -y && apt-get install -y gcc g++ cmake libnuma-dev wget git curl jq

# 设置全局pip镜像源为清华源，加速Python包下载，避免官方源的速度限制
pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```



##### 2. 配置额外的PyPI镜像源

```bash
# 针对PyTorch的CPU版本和华为昇腾NPU的Python包
# global.extra-index-url：设置额外的包索引URL（与主索引并行搜索）；多个URL用空格分隔
# 提供PyTorch的CPU版本安装包：
# 1.x86架构机器（没有NPU硬件）；2.开发测试环境（不需要GPU/NPU加速）；3.torch-npu的开发版本依赖
# 提供华为昇腾相关的Python包：
# 1.torch-npu：PyTorch的昇腾NPU版本；2.torchvision-npu：计算机视觉库的NPU版本；3.apex：混合精度训练工具；4.其他昇腾生态相关的Python包
pip config set global.extra-index-url "https://download.pytorch.org/whl/cpu/ https://mirrors.huaweicloud.com/ascend/repos/pypi"
```



##### 3. 从**预编译的 wheel 包**安装 vllm和 vllm-ascend

```bash
# Install vllm-project/vllm from pypi
# 来自vLLM项目的核心库
pip install vllm==0.10.2

# Install vllm-project/vllm-ascend from pypi.
# 专门为华为昇腾NPU优化的版本
# vllm-ascend依赖vllm，vllm提供基础框架和CPU/GPU支持，vllm-ascend添加昇腾NPU后端支持
pip install vllm-ascend==0.10.2rc1
```



##### 4. 安装阿里巴巴的ModelScope库

```bash
# ModelScope：阿里巴巴达摩院推出的模型即服务(MaaS)平台，提供海量预训练模型的统一访问接口，支持模型推理、微调、部署等全流程
# 验证安装时识别Qwen模型
pip install modelscope>=1.18.1
```



### 验证安装

```python
# LLM: 大型语言模型类，负责加载和运行模型
# SamplingParams: 采样参数类，控制文本生成的行为
from vllm import LLM, SamplingParams

# 包含4个不同的文本补全任务
prompts = [
    "Hello, my name is",
    "The president of the United States is",
    "The capital of France is",
    "The future of AI is",
]

# 配置采样参数
# temperature（控制生成随机性）：值越高（接近1.0）输出越随机有创意，值越低（接近0）输出越确定和保守
# top_p（核采样(nucleus sampling)）：只从概率累积达到95%的词汇中选择，平衡生成质量和多样性
sampling_params = SamplingParams(temperature=0.8, top_p=0.95)

# 加载语言模型
llm = LLM(model="Qwen/Qwen2.5-0.5B-Instruct")

# 执行文本生成
outputs = llm.generate(prompts, sampling_params)
# 处理并输出结果
for output in outputs:
    prompt = output.prompt
    generated_text = output.outputs[0].text
    print(f"Prompt: {prompt!r}, Generated text: {generated_text!r}")
```

