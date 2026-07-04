# 19. CUDA

CUDA is NVIDIA's programming platform for running code on NVIDIA GPUs.

Most application developers do not write CUDA directly. However, many AI frameworks and inference libraries depend on CUDA underneath.

## Why CUDA Matters

When you use PyTorch on an NVIDIA GPU, CUDA is usually doing the low-level GPU work. CUDA handles launching GPU kernels, moving data, and using GPU compute units.

If CUDA, drivers, and library versions do not match, model serving can fail.

## Drivers And Runtime

GPU software has layers:

- GPU driver
- CUDA runtime
- Libraries such as cuBLAS and cuDNN
- Frameworks such as PyTorch
- Serving engines such as vLLM or TensorRT-LLM

Version compatibility matters across these layers.

## Kernels

A GPU kernel is a function that runs on the GPU. Inference frameworks use optimized kernels for matrix multiplication, attention, normalization, and other model operations.

Better kernels can significantly improve speed.

## Key Ideas

- CUDA is the low-level platform for NVIDIA GPU computing.
- AI frameworks rely on CUDA libraries.
- Version compatibility is a common deployment issue.
- Optimized kernels improve inference performance.

## Developer Checklist

- Record driver, CUDA, framework, and serving engine versions.
- Use tested container images when possible.
- Avoid changing GPU software versions casually.
- Benchmark after upgrades.

