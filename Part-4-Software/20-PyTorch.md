# 20. PyTorch

PyTorch is a popular framework for building and running deep learning models.

Researchers and engineers use PyTorch because it is flexible and has a strong ecosystem.

## PyTorch In The AI Workflow

PyTorch is commonly used for:

- Model development
- Training
- Fine-tuning
- Experimentation
- Exporting models
- Simple inference

Many model repositories provide PyTorch weights or code.

## Tensors And Devices

PyTorch uses tensors for numerical data. A tensor can live on CPU or GPU.

A common beginner mistake is mixing tensors on different devices. If the model is on GPU but the input is on CPU, the program may fail or move data slowly.

## Eager Execution

PyTorch is easy to debug because operations run in a direct, Python-friendly way. This helps development, but raw PyTorch may not be the fastest serving option for high-volume inference.

## PyTorch In Production

PyTorch can serve models directly, especially for smaller workloads. For large LLM serving, teams often use specialized engines that optimize batching, KV cache, and scheduling.

## Key Ideas

- PyTorch is a core deep learning framework.
- It is excellent for development and experimentation.
- Production serving may need additional optimization.
- Device placement matters.

## Developer Checklist

- Know whether tensors are on CPU or GPU.
- Use `torch.no_grad()` or inference mode for inference code.
- Benchmark raw PyTorch against serving engines for LLM workloads.
- Keep model loading and request handling separate.

