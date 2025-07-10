# 🚀 vLLM Ubuntu安装向导

![Ubuntu](https://img.shields.io/badge/Ubuntu-20.04+-orange.svg)
![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![CUDA](https://img.shields.io/badge/CUDA-11.8+-green.svg)
![vLLM](https://img.shields.io/badge/vLLM-latest-purple.svg)

[English](README.md) | [中文](README_CN.md)

> 🎯 这是一个模块化的vLLM安装指南，根据你的具体情况选择对应的安装步骤。

---

## 📚 目录导航

### 🔍 准备阶段
- **[📋 硬件要求](#-硬件要求必须满足)** - 检查你的硬件是否满足要求
- **[📋 推荐软件版本组合](#-推荐软件版本组合)** - 选择合适的版本搭配
- **[🛣️ 安装路径选择](#️-安装路径选择)** - 根据你的情况选择安装方式
  - [情况1: 全新系统（推荐新手）](#-情况1-全新系统推荐新手)
  - [情况2: 已有CUDA环境](#-情况2-已有cuda环境)
  - [情况3: 有PyTorch环境](#-情况3-有pytorch环境)

### 📖 详细安装指南
- **[📋 基础依赖安装](docs/01-basic-dependencies.md)** - 系统包和工具
- **[🎮 NVIDIA驱动安装](docs/02-nvidia-drivers.md)** - GPU驱动配置
- **[⚡ CUDA工具包安装](docs/03-cuda-installation.md)** - CUDA开发环境
- **[🐍 Python环境配置](docs/04-python-setup.md)** - Python版本检查
- **[📦 vLLM安装](docs/05-vllm-installation.md)** - 虚拟环境、PyTorch和vLLM完整安装
- **[✅ 验证测试](docs/06-verification.md)** - 安装验证

### ✅ 验证和优化
- **[✅ 安装完成后的验证](#-安装完成后的验证)** - 确认安装成功

---

## 📋 硬件要求（必须满足）

### **基本要求：**
- **CPU**: 至少4核心，推荐8核心以上
- **内存**: 至少16GB，推荐32GB或更多
- **存储**: 
  - **系统盘**: 至少50GB可用空间
  - **模型存储**: 200GB-2TB（取决于模型大小）
    - 7B模型: ~15GB
    - 13B模型: ~25GB  
    - 70B模型: ~140GB
    - 多个模型或微调: 500GB+
- **网络**: 稳定的网络连接（首次下载模型需要）

### **GPU要求（关键）：**
- **必须**: NVIDIA GPU（AMD GPU支持有限）
- **计算能力**: 7.0或更高
- **显存要求**:
  - 小模型测试（125M-1B参数）: 4-6GB显存
  - 中等模型（1B-7B参数）: 8-16GB显存
  - 大模型（7B-13B参数）: 16-24GB显存
  - 超大模型（30B-70B参数）: 48GB+显存或多GPU

### **支持的GPU型号：**
- ✅ RTX 4090 (24GB) - 推荐，可运行13B模型
- ✅ RTX 4080 (16GB) - 适合7B-13B模型
- ✅ RTX 3090/3090Ti (24GB) - 13B模型良好支持
- ✅ RTX 3080/3080Ti (10-12GB) - 7B模型推荐
- ✅ RTX 3060 Ti/3070 (8-10GB) - 小模型和实验
- ✅ Tesla V100/A100/H100 - 服务器级别
- ⚠️ RTX 2060/2070 (6-8GB) - 仅小模型
- ❌ GTX 1050/1050 Ti (4GB) - 计算能力不足

---

## 📋 推荐软件版本组合

为了确保最佳兼容性和性能，建议使用以下版本组合：

### 🥇 **推荐组合1（最新稳定）**
| 组件 | 推荐版本 | 说明 |
|------|----------|------|
| **Ubuntu** | 22.04 LTS | 最新LTS版本，支持最好 |
| **Python** | 3.11.x | 性能最佳，兼容性好 |
| **NVIDIA驱动** | 535.x+ | 支持最新GPU和CUDA |
| **CUDA** | 12.1 | 最新稳定版本 |
| **PyTorch** | 2.1.x+ | 支持CUDA 12.1 |
| **vLLM** | 最新版 | 最新功能和修复 |

### 🥈 **推荐组合2（保守稳定）**
| 组件 | 推荐版本 | 说明 |
|------|----------|------|
| **Ubuntu** | 20.04 LTS | 稳定性最佳 |
| **Python** | 3.10.x | 长期支持版本 |
| **NVIDIA驱动** | 470.x+ | 稳定驱动版本 |
| **CUDA** | 11.8 | 广泛支持的版本 |
| **PyTorch** | 2.0.x | 稳定的PyTorch版本 |
| **vLLM** | 0.2.7+ | 经过验证的版本 |

### 🎯 **RTX 4090用户特别推荐**
| 组件 | 推荐版本 | 说明 |
|------|----------|------|
| **Ubuntu** | 22.04 LTS | 支持最新硬件 |
| **Python** | 3.11.x | 最佳性能 |
| **NVIDIA驱动** | 535.129.03+ | RTX 4090最佳驱动 |
| **CUDA** | 12.1 | 充分利用RTX 4090 |
| **PyTorch** | 2.1.0+cu121 | 专门为CUDA 12.1编译 |
| **vLLM** | 最新版 | 最佳RTX 4090支持 |

### ⚠️ **版本兼容性注意事项**
- CUDA版本必须与PyTorch版本匹配
- 驱动版本必须支持所选的CUDA版本
- Python 3.12尚不完全支持所有ML库
- 避免使用开发版本（dev/nightly）在生产环境

---

## 🛣️ 安装路径选择

根据你的系统状态，选择最适合的安装路径：

### 🆕 情况1: 全新系统（推荐新手）
你的系统刚安装，什么都没有配置：

1. **[📋 基础依赖安装](docs/01-basic-dependencies.md)** - 安装必要的系统包
2. **[🎮 NVIDIA驱动安装](docs/02-nvidia-drivers.md)** - 安装GPU驱动
3. **[⚡ CUDA工具包安装](docs/03-cuda-installation.md)** - 安装CUDA开发环境
4. **[🐍 Python环境配置](docs/04-python-setup.md)** - 检查Python版本
5. **[📦 vLLM安装](docs/05-vllm-installation.md)** - 虚拟环境、PyTorch和vLLM完整安装
6. **[✅ 验证测试](docs/06-verification.md)** - 验证安装是否成功

### 🔧 情况2: 已有CUDA环境
你已经安装了NVIDIA驱动和CUDA：

1. **[🐍 Python环境配置](docs/04-python-setup.md)**
2. **[📦 vLLM安装](docs/05-vllm-installation.md)** - 虚拟环境、PyTorch和vLLM完整安装
3. **[✅ 验证测试](docs/06-verification.md)**

### 🚀 情况3: 有PyTorch环境
你已经有了PyTorch环境：

1. **[📦 vLLM安装](docs/05-vllm-installation.md)** - 仅安装vLLM部分
2. **[✅ 验证测试](docs/06-verification.md)**

---

## ✅ 安装完成后的验证

完成所有安装步骤后，请务必运行完整的环境验证：

**[🔍 完整环境验证脚本](docs/06-verification.md)** - 一次性检查所有组件是否正确安装

这个验证脚本会检查：
- ✅ 系统信息和硬件兼容性
- ✅ Python环境和虚拟环境
- ✅ NVIDIA驱动和GPU状态  
- ✅ CUDA工具包和版本兼容性
- ✅ PyTorch安装和GPU支持
- ✅ vLLM安装和功能测试
- ✅ 系统资源和性能评估

### ⚡ 快速验证命令

```bash
# 激活虚拟环境
cd ~/vllm-learning
source vllm-env/bin/activate

# 基础功能测试
python -c "
import torch
import vllm
print(f'✅ PyTorch版本: {torch.__version__}')
print(f'✅ CUDA可用: {torch.cuda.is_available()}')
print(f'✅ GPU数量: {torch.cuda.device_count()}')
if torch.cuda.is_available():
    print(f'✅ GPU型号: {torch.cuda.get_device_name(0)}')
    print(f'✅ 显存: {torch.cuda.get_device_properties(0).total_memory // 1024**3}GB')
print(f'✅ vLLM版本: {vllm.__version__}')
print('🎉 环境配置成功！')
"
```

如果所有检查都通过，说明你的vLLM环境配置完美！

---

## 🤝 贡献指南

欢迎提交改进建议！请确保：

1. 🔍 测试你的修改
2. 📝 更新相关文档
3. 📋 提交详细的PR描述

---

## 📄 许可证

本项目采用 [MIT License](LICENSE) 许可证。

---

<div align="center">

**🌟 如果这个项目对你有帮助，请给个Star！🌟**

**📚 选择你的安装路径，开始vLLM学习之旅吧！**

Made with ❤️ by [Christina](https://github.com/christinazhang139)

</div>
