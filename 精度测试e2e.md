##### 1. 创建隔离的容器环境，映射昇腾设备

```bash
## 1.环境变量设置 (Environment Variable Setup)
# 设置一个名为 IMAGE 的环境变量，其值是Docker镜像的完整路径和标签。

## 2.docker运行命令 (Docker Run Command)
# -i (interactive): 保持标准输入打开(通常与-t联用); -t (tty): 分配一个伪终端，允许交互式操作;  -d (detach): 后台 (分离模式) 运行容器，并打印容器 ID
# --name : 定义容器名称
# --net=host : 容器使用主机 (Host)的网络命名空间。这意味着容器内的应用程序可以直接访问主机网络接口，端口映射不再需要 (但在命令中仍有 -p 选项，这在这种情况下是冗余的，除非它用于记录或脚本的可移植性)
# -e ASCEND_VISIBLE_DEVICES=0,1,2,... : 设置环境变量，指定容器内可见和可用的昇腾设备ID
# 显式地将主机上的16个昇腾NPU核心设备 (/dev/davinciX) 映射到容器内。这是运行在昇腾上的AI应用必需的操作

## 3.设备映射 (Device Mapping)
# --device /dev/davinci_manager : 映射昇腾设备管理相关的设备文件
# --device /dev/devmm_svm : 映射与内存管理(Shared Virtual Memory)相关的设备文件，通常用于高性能计算
# --device /dev/hisi_hdc : 映射华为海思 (Hisi)的HDC(Host Device Communication)设备文件，用于主机和设备间的通信

## 4.卷挂载 (Volume Mounts)
# 使用 -v host_path:container_path 将主机目录或文件挂载到容器内，实现数据共享和访问主机上的驱动/工具

## 5.端口映射与应用配置 (Port Mapping & App Config)
# -p 8004:8004 : 将容器的 8004 端口 映射到主机的 8004 端口。这是 vLLM 服务常用的端口。注意：由于使用了 --net=host，此选项通常是冗余的，但在某些环境中可能出于兼容性或规范目的保留。
# -e VLLM_USE_MODELSCOPE=True : 设置环境变量，告诉 vLLM 使用 ModelScope 作为模型源或配置。ModelScope 是一个 AI 模型社区和平台
# -e PYTORCH_NPU_ALLOC_CONF=max_split_size_mb:256 : 设置PyTorch(在昇腾上通常使用 PyTorch/NPU)的内存分配配置，指定最大分割大小为256MB，可能用于优化内存碎片和性能
# -it $IMAGE : 指定要运行的镜像，即之前设置的$IMAGE变量的值
# /bin/bash	: 这是容器启动后要执行的命令。它会启动一个Bash shell。由于使用了-itd，这会在后台启动一个可交互的shell进程 (虽然是后台，但进程本身是 shell)，容器启动后会停留在shell状态，允许用户通过docker attach或docker exec进入容器进行进一步操作

export IMAGE=m.daocloud.io/quay.io/ascend/vllm-ascend:v0.11.0rc0-a3
docker run -itd \
--name zsl_node2 \
--net=host \
-e ASCEND_VISIBLE_DEVICES=0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15 \
--device /dev/davinci0 \
--device /dev/davinci1 \
--device /dev/davinci2 \
--device /dev/davinci3 \
--device /dev/davinci4 \
--device /dev/davinci5 \
--device /dev/davinci6 \
--device /dev/davinci7 \
--device /dev/davinci8 \
--device /dev/davinci9 \
--device /dev/davinci10 \
--device /dev/davinci11 \
--device /dev/davinci12 \
--device /dev/davinci13 \
--device /dev/davinci14 \
--device /dev/davinci15 \
--device /dev/davinci_manager \
--device /dev/devmm_svm \
--device /dev/hisi_hdc \
-v /usr/local/dcmi:/usr/local/dcmi \
-v /usr/local/Ascend/driver/tools/hccn_tool:/usr/local/Ascend/driver/tools/hccn_tool \
-v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \
-v /usr/local/Ascend/driver/lib64/:/usr/local/Ascend/driver/lib64/ \
-v /usr/local/Ascend/driver/version.info:/usr/local/Ascend/driver/version.info \
-v /etc/ascend_install.info:/etc/ascend_install.info \
-v /mnt/sfs_turbo/ascend-ci-share-nv-action-vllm-benchmarks:/root/.cache \
-p 8004:8004 \
-e VLLM_USE_MODELSCOPE=True \
-e PYTORCH_NPU_ALLOC_CONF=max_split_size_mb:256 \
-it $IMAGE \
/bin/bash
```

##### 2.进入容器，配置环境

```bash
docker exec -it <id> bash

cd /vllm-workspace/vllm-ascend

export VLLM_USE_MODELSCOPE=True

# 配置 Git 的全局设置，将所有指向 https://github.com/ 的请求重定向或替换为通过 https://ghfast.top/ 的路径。这个操作通常是为了加速在中国境内访问GitHub仓库的速度和稳定性，特别是在进行git clone或git pull操作时
git config --global url."https://ghfast.top/https://github.com/".insteadOf "https://github.com/"

# 将pip的主要索引URL配置为清华大学(Tsinghua)的PyPI镜像站
pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple

# 设置一个额外的索引URL，指向华为云(Huawei Cloud)的昇腾(Ascend)软件包仓库。这对于安装任何特定于昇腾NPU的库（如PyTorch/NPU相关的包）至关重要。
export PIP_EXTRA_INDEX_URL=https://mirrors.huaweicloud.com/ascend/repos/pypi

```

##### 3. 在线服务（命令行）

```bash
# vllm serve: 启动vLLM的API服务器
# Qwen/Qwen2.5-0.5B-Instruct: 指定要加载和部署的模型名称
# --max_model_len 4096: 设置模型可以处理的最大序列长度（上下文长度）为4096个token
# &: 将服务命令放在后台运行，以便用户可以继续在当前终端中执行后续的评估命令

# export HF_ENDPOINT=... 设置环境变量HF_ENDPOINT，将Hugging Face模型的下载地址重定向到 hf-mirror.com。这是一个常用的Hugging Face镜像站，用于加速模型文件在中国的下载速度
# pip install lm-eval[api]: 使用pip安装lm-eval库。lm-eval是一个用于评估大型语言模型 (LLM) 在各种基准测试上性能的工具。[api]表示安装了用于通过API与本地或远程服务进行通信所需的额外依赖项，这正是评估vLLM服务的关键

# 指定评估时使用的模型类型。local-completions表明评估器将通过API与一个本地运行的文本补全服务进行交互，而不是直接加载模型权重
# model=Qwen/Qwen2.5-0.5B-Instruct: 用于向API服务（vLLM）传递的模型名称或标识符
# base_url=http://127.0.0.1:8000/v1/completions: 指定vLLM服务API的端点地址。默认情况下，vLLM API服务运行在8000端口
# tokenized_requests=False: 指示lm-eval不要在客户端进行tokenization，而是将原始文本发送给服务器，让vLLM服务处理tokenization
# trust_remote_code=True: 在加载或使用模型时，允许执行模型仓库中的自定义Python代码（对于 Qwen模型通常是必需的）
# --tasks gsm8k: 指定要运行的评估任务/数据集。gsm8k 是一个评估模型数学推理能力的基准测试数据集
# --output_path ./	指定评估结果（如准确率、损失等）的输出目录，这里是当前目录

# online server
vllm serve Qwen/Qwen2.5-0.5B-Instruct --max_model_len 4096 &

export HF_ENDPOINT="https://hf-mirror.com"
pip install lm-eval[api]

# Only test gsm8k dataset in this demo
lm_eval \
  --model local-completions \
  --model_args model=Qwen/Qwen2.5-0.5B-Instruct,base_url=http://127.0.0.1:8000/v1/completions,tokenized_requests=False,trust_remote_code=True \
  --tasks gsm8k \
  --output_path ./
```

##### 4. 离线服务（命令行）

```bash
# 指定评估使用的模型类型/后端为vllm。这指示 lm-eval 直接使用 vLLM 库作为其底层的推理引擎，实现高性能的吞吐量
# pretrained=Qwen/Qwen2.5-0.5B-Instruct: 指定vLLM要加载的预训练模型名称
# 设置推理的批处理大小(batch size)。设置为auto时，lm-eval会让vLLM动态地确定和管理最佳的批处理大小，以最大化GPU/NPU的吞吐量
# 设置评估任务的数据限制。这指示lm-eval只使用gsm8k数据集中的前100个样本进行测试。这通常用于快速验证配置或进行快速测试，而不是进行完整的基准测试

# offline server
export HF_ENDPOINT="https://hf-mirror.com"
pip install lm-eval

# Only test gsm8k dataset in this demo
lm_eval \
  --model vllm \
  --model_args pretrained=Qwen/Qwen2.5-0.5B-Instruct,max_model_len=4096 \
  --tasks gsm8k \
  --batch_size auto
  --limit 100
```

##### 5. yaml文件配置

```yaml
model_name: "baichuan-inc/Baichuan2-13B-Chat"

# tensor_parallel_size: 1 # TP1是默认值，可不写

# 任务和指标 (参考Qwen3-30B-A3B.yaml)
# 假设进行常见的数学推理 (gsm8k) 和中文综合能力测试 (ceval-valid)
tasks:
- name: "gsm8k"
  metrics:
  # 这里的value需要实际测试后填充，我用问号占位
  - name: "exact_match,strict-match"
    value: 0.5
  - name: "exact_match,flexible-extract"
    value: 0.5
- name: "ceval-valid"
  metrics:
  - name: "acc,none"
    value: 0.5

# 运行参数配置
# Baichuan2-13B-Chat 是一个Chat模型，通常需要应用聊天模板
apply_chat_template: False
fewshot_as_multiturn: False # 聊天模型通常将fewshot视为多轮对话

# 其他性能和环境参数
num_fewshot: 5
# 13B模型，单卡运行时可能需要较高的显存占用率
gpu_memory_utilization: 0.9
# Baichuan模型可能需要信任远程代码
trust_remote_code: True
```

##### 6. 命令行命令和脚本命令

lm-eval: 
(文本vllm, 多模态vllm-vlm)

```bash
# 配置张量并行（Tensor Parallelism）大小为 4。这指示vLLM将模型的权重和计算分布到4个GPU或NPU(昇腾) 设备上，以加速推理和处理更大的模型

# --apply_chat_template: 指示lm-eval在将提示词发送给模型之前，应用该模型（这里是Qwen）的官方聊天模板。这确保了评估提示词的格式与模型训练时的对话格式保持一致，从而提高性能的准确性
# 没有应用模板 (错误或低效):[5个示例...] 问：新的问题
# 应用模板 (高效且正确):
# <|im_start|>system
# 你是一个有帮助的助手。
# <|im_end|>
# <|im_start|>user
# [示例1问题]
# <|im_end|>
# <|im_start|>assistant
# [示例1答案]
# <|im_end|>
# ...
# <|im_start|>user
# 约翰有5个苹果...
# <|im_end|>
# <|im_start|>assistant

# --fewshot_as_multiturn: 少数样本学习 (Few-Shot Learning) 的配置，指示将少数样本示例作为多轮对话的格式来构建提示词。这与聊天模板一起，确保模型在更自然的对话上下文中接收提示
# --num_fewshot 5: 设置少数样本学习的样本数量为5。这意味着在评估每个问题之前，模型将获得5个示例作为上下文来指导其回答
pip install lm_eval
lm_eval \
	--model vllm \
    --model_args pretrained=/root/.cache/modelscope/hub/models/Qwen/Qwen2.5-VL-7B-Instruct,max_model_len=4096,tensor_parallel_size=4 \
    --tasks gsm8k --apply_chat_template --fewshot_as_multiturn --batch_size auto \
    --num_fewshot 5  &
```

脚本：

```bash
export VLLM_COMMIT="26b999c"  # 指定上游vLLM仓库使用的特定Git Commit版本，确保代码一致
export VLLM_ASCEND_COMMIT="6940870"  # 指定vLLM-Ascend分支或修改使用的特定Git Commit版本

export GHA_CANN_VERSION="8.2.RC1"  # 指定CANN的版本
export GHA_TORCH_VERSION="2.7.1"  # 指定 PyTorch 的版本
export GHA_TORCH_NPU_VERSION="2.7.1.dev20250724"  # 指定PyTorch针对昇腾NPU的定制版本
export GHA_VLLM_VERSION="0.11.0"  # 指定vLLM的版本号

export VLLM_WORKER_MULTIPROC_METHOD="spawn"  # 设置vLLM多进程方法为spawn
export VLLM_USE_MODELSCOPE="true"  # 开启 vLLM对ModelScope的支持
export VLLM_VERSION="0.11.0"  # 再次指定vLLM的版本号
export VLLM_ASCEND_VERSION="refs/pull/2917/merge"  # 可能是一个Git分支引用或合并请求(Pull Request)的引用，指示正在测试的昇腾特定代码源

# 重复指定CANN, PyTorch和PyTorch/NPU的版本
export CANN_VERSION="8.2.RC1"
export TORCH_VERSION="2.7.1"
export TORCH_NPU_VERSION="2.7.1.dev20250724"

mkdir -p ./benchmarks/accuracy  # 创建目录用于存储模型准确性测试的结果

# -s: 允许测试时输出print或logging语句，方便调试
# -v: 增加输出的详细程度(Verbose)，显示测试函数名等信息
# .../_.py: 指定要运行的测试文件。这个文件负责执行一个端到端 (E2E)测试，核心是验证vLLM对模型的推理结果是否与预期的准确性相符（通常是通过lm-eval库）
# -config: 一个自定义的pytest或测试脚本参数，用于指定配置文件的路径
# Qwen2.5-VL-7B-Instruct.yaml: 这个YAML文件包含了运行Qwen2.5-VL-7B-Instruct模型所需的所有 测试参数，例如：要测试哪个任务（如 gsm8k）、预期的准确性阈值、模型路径、Few-Shot设置等
pip install lm_eval
pip install pytest
pytest -sv ./tests/e2e/models/test_lm_eval_correctness.py \
--config ./tests/e2e/models/configs/Baichuan2-13B-Chat.yaml
```





