# 📋 基础依赖安装

[← 返回主页](../README_CN.md) | [下一步: NVIDIA驱动安装 →](02-nvidia-drivers.md)

> 🎯 安装运行vLLM所需的基础系统包和工具。

---

## ⚡ 快速安装

```bash
# 更新系统包
sudo apt update && sudo apt upgrade -y

# 安装必要的工具
sudo apt install -y \
    git \
    curl \
    wget \
    vim \
    htop \
    tree \
    build-essential
```

## ✅ 验证安装

```bash
# 检查关键组件
git --version
gcc --version
```

**期望输出:**
```
git version 2.34.1
gcc (Ubuntu 11.4.0) 11.4.0
```

---

## 🚀 下一步

根据你的情况选择:

- **[🎮 安装NVIDIA驱动](02-nvidia-drivers.md)** - 如果你有NVIDIA GPU（推荐）
- **[🐍 配置Python环境](04-python-setup.md)** - 如果你已有GPU驱动，可直接配置Python
