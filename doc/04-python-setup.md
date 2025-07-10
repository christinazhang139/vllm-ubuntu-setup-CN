# 🐍 Python环境配置

[← 上一步: CUDA安装](03-cuda-installation.md) | [下一步: vLLM安装 →](05-vllm-installation.md)

> 🎯 检查和安装vLLM所需的Python版本。

---

## 🔍 Python版本要求

| 组件 | 最低版本 | 推荐版本 | 状态 |
|------|----------|----------|------|
| **Python** | 3.8+ | 3.11.x | 🟢 最佳性能 |
| **pip** | 20.0+ | 最新版 | 🟢 自动包含 |

---

## ✅ 检查当前Python版本

```bash
# 检查Python版本
python3 --version

# 检查pip版本
pip3 --version
```

**期望输出:**
```bash
Python 3.11.x (推荐)
# 或
Python 3.10.x (可用)
# 或  
Python 3.9.x (可用)
```

---

## 🔧 版本检查结果

### ✅ 版本满足要求（Python 3.8+）
```bash
# 如果版本 >= 3.8，可以继续安装
echo "✅ Python版本满足要求，可以继续下一步"
```

---

## 🚀 下一步

Python环境确认完成后：

**[📦 vLLM安装 →](05-vllm-installation.md)**

> 💡 **提醒**: 下一步将创建虚拟环境并安装PyTorch和vLLM，确保选择与你的CUDA版本匹配的PyTorch版本。
