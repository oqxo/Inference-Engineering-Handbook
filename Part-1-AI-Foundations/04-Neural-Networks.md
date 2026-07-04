# 04. Neural Networks

A neural network is a model made of layers of simple mathematical operations.

The name comes from biology, but production engineers should think of it as a large computation graph. Data flows in, numbers are multiplied and transformed, and output comes out.

## Tensors

Neural networks operate on tensors. A tensor is a container of numbers. It can be a single number, a list, a matrix, or a higher-dimensional block of numbers.

Examples:

- A text token can become a vector of numbers.
- An image can become a grid of pixel values.
- Audio can become a sequence of signal values.

Frameworks such as PyTorch represent model data as tensors.

## Weights And Activations

Weights are learned values stored in the model. Activations are intermediate values created while the model processes an input.

During inference, both matter:

- Weights must fit in memory.
- Activations use temporary memory.
- Large requests create more activations.
- Long context creates more memory pressure.

## Forward Pass

When a model processes input and produces output, it performs a forward pass.

For inference, we only need the forward pass. Training also performs backward calculations to update weights, but inference does not.

This is one reason inference is usually cheaper than training. However, inference can still be expensive at high traffic.

## Why It Matters For Inference

Neural networks are not like normal request handlers. The same model may behave very differently depending on input length, batch size, hardware, precision, and caching.

The inference engineer must understand the model as both software and computation.

## Key Ideas

- Neural networks are computation graphs.
- Tensors are containers of numbers.
- Weights are learned model values.
- Activations are temporary values during computation.
- Inference runs the forward pass.

## Developer Checklist

- Track model weight memory and runtime memory separately.
- Watch GPU memory, not only CPU memory.
- Treat long inputs as more expensive than short inputs.
- Benchmark with realistic input and output lengths.

