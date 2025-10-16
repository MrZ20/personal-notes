#### 提交PR：精度测试

```bash
## 1.fork分支到自己的账号

## 2.从自己账号上将分支clone到本地
# 注：本地地址不用双引号会被吞掉\，或者打开到文件夹内再克隆
git clone -b <分支名称> --single-branch <仓库URL> [本地文件夹名称]

## 3.使用vscode上的源代码管理打开
# 如果本地有git，需要在vscode上添加环境路径，将git.exe的路径传给vscode
# 终端要使用git，进入windows的"编辑系统环境变量"，然后找到系统变量中的"path"，在里面添加".../cmd"

## 4.编写相关文档
```

```yaml
# (1) .github/workflows/accurary_test.yaml
# accurary_test.yaml:一个GitHub Actions工作流（Workflow）的YAML配置文件。它的核心作用是为vllm-ascend项目设置一个自动化的准确性（accuracy）测试流程，特别针对提交到主分支或开发分支的拉取请求（Pull Request, PR）
# 主要修改：
jobs:
  run:
    name: ""
    strategy:
      # 使用矩阵（Matrix）策略来并行测试多个模型
      matrix:
        # Only top series models should be listed in here
        # runner: 指定运行测试的昇腾硬件环境的类型（a2-1或a2-2）
        # model_name: 要测试的具体模型名称
        include:
          - runner: a2-1
            model_name: Qwen3-8B
          - runner: a2-1
            model_name: Qwen2.5-VL-7B-Instruct
          - runner: a2-1
            model_name: Qwen2-Audio-7B-Instruct
          - runner: a2-2
            model_name: Qwen3-30B-A3B
          - runner: a2-2
            model_name: Qwen3-VL-30B-A3B-Instruct
          - runner: a2-2
            model_name: DeepSeek-V2-Lite
          - runner: a2-1
            model_name: Qwen3-VL-8B-Instruct
          - runner: <环境类型>
            model_name: <具体模型>
      # 确保即使矩阵中的某个测试失败，其他模型的测试也会继续运行
      fail-fast: false
```

```bash
# (2) test/e2e/models/configs/accurary.txt
# <具体模型>
```

```yaml
# (3)test/e2e/models/configs/<具体模型.yaml>
model_name: "Qwen/Qwen3-VL-8B-Instruct"
runner: "linux-aarch64-a2-1"
hardware: "Atlas A2 Series"
model: "vllm-vlm"
tasks:
- name: "mmmu_val"
  metrics:
  - name: "acc,none"
    value: 0.55
max_model_len: 8192
batch_size: 32
gpu_memory_utilization: 0.7

```

```bash
# 5.上传github分支
git add .
git commit --amend -s --no-verify
# --amend:它不会创建一个新的提交，而是将暂存区的内容（如果有）和上一次提交的内容合并起来，替换掉上一次提交
# -s:在提交信息中自动添加一行 Signed-off-by: Your Name <your-email>;通常用于表明开发者同意其贡献符合项目的贡献许可协议（例如DCO-Developer Certificate of Origin）
# --no-verify:提交时跳过 Git 客户端的本地钩子（Hooks），特别是 pre-commit 钩子。这些钩子通常用于运行代码风格检查、单元测试等，跳过它意味着忽略这些检查
git push -f origin ZengSilong
# -f:强制推送。它会覆盖远程分支的历史记录，即使远程分支包含您本地没有的提交。由于git commit --amend更改了历史记录（创建了一个新的提交ID来替换旧的），Git会认为本地和远程的历史是冲突的，因此必须使用-f才能成功推送
# git commit -m "messages" -s 
# git push origin <您的分支名>

# 回退
git log --oneline  # 查看日志，Q退出
git revert <版本号>  # 回退，:wq确认回退信息
git push origin <您的分支名>  # 重新推送
```

```
# 6.提交PR
格式：[Test]add accuracy test for model Qwen3-VL-8B-Instruction
在What this PR does / why we need it?中加入add accuracy test for model Qwen3-VL-8B-Instruction
```

