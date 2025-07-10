# ⚡ CUDA工具包安装

[← 上一步: NVIDIA驱动](02-nvidia-drivers.md) | [下一步: Python环境配置 →](04-python-setup.md)

> 🎯 安装CUDA开发工具包，为PyTorch和vLLM提供GPU计算支持。

---

## 🔍 选择CUDA版本

根据你的GPU选择合适的CUDA版本：

| GPU系列 | 推荐CUDA | PyTorch支持 | 说明 |
|---------|----------|-------------|------|
| **RTX 4090/4080** | **CUDA 12.1** | ✅ cu121 | 最佳平衡 |
| **RTX 4070/4060** | **CUDA 12.1** | ✅ cu121 | 稳定支持 |
| **RTX 3090/3080** | **CUDA 11.8** | ✅ cu118 | 广泛兼容 |
| **RTX 3070/3060** | **CUDA 11.8** | ✅ cu118 | 推荐版本 |

> ⚠️ **重要**: 不推荐使用最新版本（如CUDA 12.9+），因为PyTorch和vLLM可能还不支持。

> 💡 **选择原则**: 兼容性 > 最新版本。确保PyTorch有对应的cu版本支持。

---

## ⚡ 安装CUDA 12.1（RTX 40系列推荐）

```bash
# 下载CUDA 12.1安装包
wget https://developer.download.nvidia.com/compute/cuda/12.1.0/local_installers/cuda_12.1.0_530.30.02_linux.run

# 运行安装程序
sudo sh cuda_12.1.0_530.30.02_linux.run

# 在安装界面中：
# - 取消勾选Driver（已安装）
# - 保持勾选CUDA Toolkit
# - Continue安装
```

## ⚡ 安装CUDA 11.8（RTX 30系列推荐）

```bash
# 下载CUDA 11.8安装包
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run

# 运行安装程序
sudo sh cuda_11.8.0_520.61.05_linux.run

# 在安装界面中：
# - 取消勾选Driver（已安装）
# - 保持勾选CUDA Toolkit
# - Continue安装
```

---

## ✅ 验证安装

```bash
# 检查CUDA版本
nvcc --version

# 检查CUDA编译器路径
which nvcc

# 验证GPU和CUDA
nvidia-smi
```

### 🔧 如果nvcc命令不可用

```bash
# 只有在nvcc不可用时才需要设置环境变量
echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc

# 重新加载配置
source ~/.bashrc

# 再次验证
nvcc --version
```

**期望输出:**
```bash
# nvcc --version 输出示例
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Mon_Apr__3_17:16:06_PDT_2023
Cuda compilation tools, release 12.1, V12.1.105

# nvidia-smi 应显示CUDA Version
CUDA Version: 12.1
```

---

## 🚀 下一步

CUDA安装完成后：

**[🐍 配置Python环境 →](04-python-setup.md)**

> 💡 **注意**: 下一步将检查Python版本，确保满足vLLM的要求。
