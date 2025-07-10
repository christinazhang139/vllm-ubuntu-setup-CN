# ✅ 验证测试

[← 上一步: vLLM安装](05-vllm-installation.md)

> 🎯 验证vLLM环境是否正确安装和配置。

---

## ⚡ 环境验证

```bash
# 激活环境
cd ~/vllm-learning
source vllm-env/bin/activate

# 一键验证所有组件
python -c "
import torch, vllm
print(f'✅ PyTorch: {torch.__version__} (CUDA: {torch.cuda.is_available()})')
print(f'✅ vLLM: {vllm.__version__}')
print(f'✅ GPU: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else \"CPU only\"}')
print('🎉 vLLM环境配置完成！')
"
```

**期望输出:**
```
✅ PyTorch: 2.1.0+cu121 (CUDA: True)
✅ vLLM: 0.2.7
✅ GPU: NVIDIA GeForce RTX 4090
🎉 vLLM环境配置完成！
```

---

## 🚀 开始使用

环境验证成功后，你可以：

- 🔬 **运行vLLM实验**
- 📚 **学习vLLM用法**
- 🎯 **加载和测试模型**

> 💡 **提醒**: 每次使用前记得激活环境：`source ~/vllm-learning/vllm-env/bin/activate`
