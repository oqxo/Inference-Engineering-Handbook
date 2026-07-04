# 28. KV Caching

KV caching is one of the most important optimizations in LLM inference.

It stores internal attention data from previous tokens so generation does not repeat unnecessary work.

## Request-Level Cache

During a single request, the cache grows as tokens are processed and generated. This is the normal KV cache used during decode.

The longer the sequence, the more memory the cache uses.

## Prefix Cache

Some systems can reuse cached computation for shared prompt prefixes.

For example, many requests may start with the same system prompt. If the serving engine can reuse that prefix, time to first token may improve.

## Cache Pressure

KV cache competes for GPU memory with model weights and other requests. When cache memory is full, the server may need to queue, reject, or evict work.

This affects tail latency.

## Practical Limits

Long context is useful, but it is not free. A product that sends every previous message forever may waste memory and slow down inference.

## Key Ideas

- KV caching avoids repeated attention work.
- Cache memory grows with sequence length and concurrency.
- Prefix caching can help repeated prompts.
- Cache pressure affects latency and capacity.

## Developer Checklist

- Limit context and output length.
- Reuse common prefixes when supported.
- Monitor cache utilization.
- Summarize or trim old conversation history when appropriate.

