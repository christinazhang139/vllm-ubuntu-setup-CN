# 📦 vLLM安装

[← 上一步: Python环境配置](04-python-setup.md) | [下一步: 验证测试 →](06-verification.md)

> 🎯 创建虚拟环境，安装PyTorch和vLLM，完成整个vLLM环境配置。

---

## 🔍 版本选择

### 💡 CUDA和PyTorch的关系

PyTorch需要与你的CUDA版本匹配才能正确使用GPU：

- **🔗 版本绑定**: PyTorch编译时绑定特定CUDA版本
- **❌ 不匹配后果**: GPU不可用或运行错误
- **✅ 匹配好处**: 最佳性能和稳定性

### 📋 版本对应表

根据你的CUDA版本选择对应的PyTorch：

| CUDA版本 | PyTorch版本 | 适用GPU |
|----------|-------------|---------|
| **CUDA 12.1** | **cu121** | RTX 4090, RTX 4080, RTX 4070 |
| **CUDA 11.8** | **cu118** | RTX 3090, RTX 3080, RTX 3070, RTX 3060 |

> 💡 **检查CUDA版本**: 运行 `nvidia-smi` 查看右上角的"CUDA Version"

> ⚠️ **重要**: 必须安装与你的CUDA版本匹配的PyTorch，否则vLLM无法使用GPU加速

---

## 🏠 创建虚拟环境

```bash
# 创建项目目录
mkdir -p ~/vllm-learning
cd ~/vllm-learning

# 创建虚拟环境
python3 -m venv vllm-env

# 激活虚拟环境
source vllm-env/bin/activate

# 升级pip
pip install --upgrade pip
```

---

## 🔥 安装PyTorch

### 🚀 CUDA 12.1用户
```bash
# 安装PyTorch (CUDA 12.1)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

### 🚀 CUDA 11.8用户
```bash
# 安装PyTorch (CUDA 11.8)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

## 📦 安装vLLM

```bash
# 安装vLLM和必要依赖
pip install vllm transformers accelerate
```

---

## ✅ 验证安装

```bash
# 验证PyTorch
python -c "import torch; print(f'PyTorch version: {torch.__version__}'); print(f'CUDA available: {torch.cuda.is_available()}')"

# 验证vLLM
python -c "import vllm; print(f'vLLM version: {vllm.__version__}')"
```

**期望输出:**
```
PyTorch version: 2.1.0+cu121
CUDA available: True
vLLM version: 0.2.7
```

---

## 🔄 环境管理

```bash
# 每次使用前激活环境
cd ~/vllm-learning
source vllm-env/bin/activate

# 退出虚拟环境
deactivate
```

---

## 🚀 下一步

vLLM安装完成后：

**[✅ 验证测试 →](06-verification.md)**

> 💡 **提醒**: 每次使用时都需要激活虚拟环境：`source ~/vllm-learning/vllm-env/bin/activate`
