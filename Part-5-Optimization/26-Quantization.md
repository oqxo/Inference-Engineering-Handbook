# 26. Quantization

Quantization reduces the number of bits used to store or compute model values.

A model may normally use 16-bit or 32-bit numbers. Quantization may use 8-bit, 4-bit, or other compact formats.

## Why Quantization Helps

Smaller numbers use less memory. Less memory can mean:

- Larger models fit on smaller GPUs.
- More requests fit at once.
- Data moves faster.
- Cost may go down.

Quantization can also improve speed when hardware supports the chosen format efficiently.

## Quality Tradeoff

Quantization changes numerical precision. If the precision is too low or the method is poorly matched to the model, output quality can drop.

The only safe answer is measurement. Test the quantized model on real tasks.

## Weight-Only Quantization

Weight-only quantization compresses the model weights but may keep some computations in higher precision.

This can reduce memory while preserving quality better than more aggressive approaches.

## Activation Quantization

Activation quantization also compresses intermediate values during computation. It can improve performance but may require more care.

## Key Ideas

- Quantization uses smaller number formats.
- It reduces memory and may improve speed.
- It can hurt quality.
- Real task evaluation is required.

## Developer Checklist

- Compare quality before and after quantization.
- Measure memory, latency, and throughput.
- Use hardware-supported formats.
- Keep a fallback full-precision model when possible.

