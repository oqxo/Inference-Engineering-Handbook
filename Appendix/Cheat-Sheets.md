# Cheat Sheets

## Inference Request Flow

1. Receive user request.
2. Build prompt or input payload.
3. Tokenize input.
4. Run prefill.
5. Generate tokens during decode.
6. Stream or return output.
7. Validate and post-process output.
8. Record logs and metrics.

## Core Metrics

- Time to first token
- End-to-end latency
- Input tokens
- Output tokens
- Tokens per second
- Requests per second
- GPU memory usage
- GPU utilization
- Queue length
- Error rate
- Cost per request

## Common Bottlenecks

- Long prompts
- Long outputs
- Too many concurrent requests
- GPU memory exhaustion
- Poor batching
- Slow retrieval
- Cold starts
- Network transfer between GPUs or services

## First Optimizations To Try

- Reduce prompt size.
- Set output limits.
- Enable streaming.
- Use a serving engine built for LLMs.
- Batch requests where appropriate.
- Quantize only after measuring quality.
- Cache repeated safe work.

