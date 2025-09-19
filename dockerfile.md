##### Dockerfile指令

```dockerfile
FROM         # 基础镜像，当前新镜像是基于哪个镜像的
MAINTAINER   # 镜像维护者的姓名混合邮箱地址
RUN          # 容器构建时需要运行的命令
EXPOSE       # 当前容器对外保留出的端口
WORKDIR      # 指定在创建容器后，终端默认登录的进来工作目录，一个落脚点
ENV          # 用来在构建镜像过程中设置环境变量
ADD          # 将宿主机目录下的文件拷贝进镜像且ADD命令会自动处理URL和解压tar压缩包
COPY         # 类似ADD，拷贝文件和目录到镜像中！
VOLUME       # 容器数据卷，用于数据保存和持久化工作
CMD          # 指定一个容器启动时要运行的命令，dockerFile中可以有多个CMD指令，但只有最后一个生效！
ENTRYPOINT   # 指定一个容器启动时要运行的命令！和CMD一样
ONBUILD      # 当构建一个被继承的DockerFile时运行命令，父镜像在被子镜像继承后，父镜像的ONBUILD被触发
```



##### Dcokerfile文档：已配置vllm环境

```dockerfile
# 指定基础镜像，使用华为官方提供的CANN 8.2版本，基于Ubuntu 22.04和Python 3.11
# 确保环境包含华为Ascend加速卡所需的基础驱动和软件栈
FROM quay.io/ascend/cann:8.2.rc1-910b-ubuntu22.04-py3.11

# 定义一个构建参数PIP_INDEX_URL，其默认值为清华大学的 PyPI 镜像地址
# 定义一个构建参数COMPILE_CUSTOM_KERNELS，其默认值为 1（表示启用）
ARG PIP_INDEX_URL="https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple"
ARG COMPILE_CUSTOM_KERNELS=1

# 设置Debian/Ubuntu系统的前端界面为非交互模式，禁止在apt包安装过程中出现任何交互式提示对话框
# 设置环境变量，将构建参数传递给环境变量供后续使用(ARG只在构建时存在，ENV在容器运行时也存在)
ENV DEBIAN_FRONTEND=noninteractive
ENV COMPILE_CUSTOM_KERNELS=${COMPILE_CUSTOM_KERNELS}

# 更新包列表并安装必要的系统依赖，安装编译和运行所需的工具链，清理apt缓存以减少镜像大小
# -y/--yes：自动回答yes；&&：当前命令执行成功，才会执行下一个命令；\：换行符；-rf：逐个、强制
# 删除.deb文件（相当于软件安装完了，删除安装包）
# 删除元数据缓存（元数据缓存是APT包管理器的"图书馆目录"或"菜单）
RUN apt-get update -y && \
    apt-get install -y python3-pip git vim wget net-tools gcc g++ cmake libnuma-dev && \
    rm -rf /var/cache/apt/* && \
    rm -rf /var/lib/apt/lists/*

# 设置工作目录，为后续命令提供执行上下文
# 不设置：Docker默认目录（通常是/）执行、文件可能被复制到意想不到的位置、导致路径混乱和权限问题
WORKDIR /workspace

# 将当前目录的所有文件复制到容器内，将vllm-ascend项目代码添加到镜像中
# COPY . /vllm-workspace/vllm-ascend/
# 替换原始的 COPY. 指令，使用 git clone "调用" 源代码，解决了构建过程依赖本地文件的问题
ARG VLLM_ASCEND_REPO=https://github.com/vllm-project/vllm-ascend.git
ARG VLLM_ASCEND_TAG=main
RUN git clone --depth 1 $VLLM_ASCEND_REPO --branch $VLLM_ASCEND_TAG /vllm-workspace/vllm-ascend

# 配置pip使用指定的镜像源，加速Python包下载
# pip config set：pip配置设置命令；global.index-url：设置全局的包索引URL
RUN pip config set global.index-url ${PIP_INDEX_URL}

# 克隆指定版本的vLLM仓库，获取vLLM框架源代码
ARG VLLM_REPO=https://github.com/vllm-project/vllm.git
ARG VLLM_TAG=v0.10.2
# git clone：Git版本控制系统的克隆命令
# --depth 1：浅克隆，只获取最近的一次提交
# $VLLM_REPO：仓库URL
# --branch $VLLM_TAG：指定分支或标签（之前定义为v0.10.2）
# /vllm-workspace/vllm：目标目录路径
RUN git clone --depth 1 $VLLM_REPO --branch $VLLM_TAG /vllm-workspace/vllm

# 设置VLLM_TARGET_DEVICE="empty"避免安装CUDA相关依赖
# 确保安装CPU版本的PyTorch，避免安装GPU版本
# 在Ascend环境下triton无法正常工作，需要卸载
# 删除pip下载的临时文件和缓存包
RUN VLLM_TARGET_DEVICE="empty" python3 -m pip install -v -e /vllm-workspace/vllm/ --extra-index https://download.pytorch.org/whl/cpu/ && \
    python3 -m pip uninstall -y triton && \
    python3 -m pip cache purge

# 安装vllm-ascend适配层，设置华为Ascend的PyPI镜像源，加载Ascend环境变量，添加Ascend开发库路径到LD_LIBRARY_PATH，安装vllm-ascend包(使vLLM能在Ascend设备上运行)
# export只在当前行执行有效，新的RUN指令是新的shell会话
RUN export PIP_EXTRA_INDEX_URL=https://mirrors.huaweicloud.com/ascend/repos/pypi && \
    source /usr/local/Ascend/ascend-toolkit/set_env.sh && \
    source /usr/local/Ascend/nnal/atb/set_env.sh && \
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/Ascend/ascend-toolkit/latest/`uname -i`-linux/devlib && \
    python3 -m pip install -v -e /vllm-workspace/vllm-ascend/ --extra-index https://download.pytorch.org/whl/cpu/ && \
    python3 -m pip cache purge

# 安装额外依赖，modelscope: 用于快速下载模型，ray: 用于多节点分布式推理，protobuf: 指定版本以避免兼容性问题
RUN python3 -m pip install modelscope 'ray>=2.47.1' 'protobuf>3.20.0' && \
    python3 -m pip cache purge

# 设置容器启动时的默认命令，启动bash shell方便用户交互使用
CMD ["/bin/bash"]
```

##### 

