# 🎮 NVIDIA驱动安装

[← 上一步: 基础依赖](01-basic-dependencies.md) | [下一步: CUDA安装 →](03-cuda-installation.md)

> 🎯 安装NVIDIA GPU驱动，这是运行vLLM的关键步骤。

---

## 🔍 检查GPU

```bash
# 检查是否有NVIDIA GPU
lspci | grep -i nvidia

# 查看推荐驱动
ubuntu-drivers devices
```

### 📊 GPU兼容性检查

```bash
# 检查GPU计算能力（安装驱动后）
nvidia-smi --query-gpu=name,compute_cap,memory.total --format=csv
```

**vLLM GPU要求:**

| GPU系列 | 计算能力 | vLLM兼容性 | 推荐CUDA |
|---------|----------|------------|----------|
| **RTX 4090/4080** | 8.9 | ✅ 完美支持 | CUDA 12.1 |
| **RTX 4070/4060** | 8.9 | ✅ 完美支持 | CUDA 12.1 |
| **RTX 3090/3080** | 8.6 | ✅ 完美支持 | CUDA 11.8 |
| **RTX 3070/3060** | 8.6 | ✅ 完美支持 | CUDA 11.8 |
| **GTX 1080 Ti** | 6.1 | ❌ **不支持** | - |
| **GTX 1070/1060** | 6.1 | ❌ **不支持** | - |

> ⚠️ **重要**: vLLM要求GPU计算能力 ≥ 7.0

---

## ⚡ 自动安装（推荐）

```bash
# 自动安装推荐驱动
sudo ubuntu-drivers autoinstall

# 重启系统
sudo reboot
```

---

## ✅ 验证安装

```bash
# 检查驱动状态
nvidia-smi

# 检查GPU详细信息
nvidia-smi --query-gpu=name,driver_version,memory.total,compute_cap --format=csv
```

**期望输出:**
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 535.129.03             Driver Version: 535.129.03   CUDA Version: 12.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0  On |                  N/A |
| 30%   45C    P8    25W / 450W |   1024MiB / 24564MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
```

> 💡 **检查兼容性**: 对照上面的GPU兼容性表格，确认你的GPU计算能力是否 ≥ 7.0

---

## 🚀 下一步

### ✅ 如果GPU支持vLLM（计算能力≥7.0）
**[⚡ 安装CUDA工具包 →](03-cuda-installation.md)**

### ❌ 如果GPU不支持vLLM
考虑以下选项:
- 🔄 **升级硬件**: 购买RTX 30/40系列GPU
- ☁️ **云服务**: 使用Google Colab Pro, AWS, Azure等
- 📚 **学习模式**: 继续学习环境配置，准备未来硬件升级
