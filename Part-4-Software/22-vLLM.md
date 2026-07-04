# 22. vLLM

vLLM is an open-source serving engine for large language models.

It focuses on efficient LLM inference, especially request scheduling and KV cache management.

## Why Serving Engines Exist

A normal web server handles requests independently. LLM inference is different because requests compete for GPU memory and compute.

A serving engine manages:

- Model loading
- Token generation
- Batching
- KV cache
- Streaming
- Request scheduling

## Paged KV Cache

vLLM is known for efficient KV cache management. The idea is to manage cache memory in blocks so many requests can share GPU memory more effectively.

This can improve throughput compared with naive serving.

## OpenAI-Compatible APIs

Many serving engines expose APIs shaped like common chat or completion APIs. This makes it easier to replace a remote API with self-hosted inference.

Compatibility is useful, but behavior still depends on the model and configuration.

## Key Ideas

- vLLM is built for LLM serving.
- It improves batching and KV cache handling.
- It is useful for self-hosting text generation models.
- Configuration and benchmarking are still required.

## Developer Checklist

- Test your exact model with vLLM.
- Measure throughput under concurrent traffic.
- Set context and output limits.
- Monitor GPU memory and request queueing.

