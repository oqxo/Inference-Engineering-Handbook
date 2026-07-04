# 21. ONNX

ONNX is an open format for representing machine learning models.

The goal of ONNX is portability. A model can be exported from one framework and run in another runtime that supports ONNX.

## Why ONNX Exists

Different teams use different frameworks. Training may happen in PyTorch, but production may use a runtime optimized for CPUs, GPUs, or edge devices.

ONNX helps move models across tools.

## ONNX Runtime

ONNX Runtime is a serving runtime that can execute ONNX models. It supports different execution providers for different hardware.

For some workloads, ONNX Runtime can provide strong production performance.

## Limitations

Not every model exports cleanly to ONNX. Dynamic shapes, custom operations, or newer model architectures may require extra work.

LLMs can be especially complex because of caching, dynamic sequence lengths, and optimized attention.

## When To Consider ONNX

Consider ONNX when:

- You need portability across runtimes.
- You serve smaller models.
- You need CPU or edge inference.
- Your model exports cleanly.

## Key Ideas

- ONNX is a portable model format.
- ONNX Runtime can run exported models.
- Export compatibility must be tested.
- LLM serving may need more specialized systems.

## Developer Checklist

- Verify numerical output after export.
- Benchmark the ONNX model, not only the original model.
- Test dynamic input shapes.
- Keep the original model artifact for debugging.

