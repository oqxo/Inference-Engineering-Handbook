# 30. Disaggregation

Disaggregation separates parts of inference work so each part can be scaled differently.

For LLMs, a common idea is separating prefill from decode.

## Why Separate Prefill And Decode

Prefill and decode have different performance shapes. Prefill processes many input tokens and can use parallel compute. Decode generates tokens sequentially and is often memory-bandwidth sensitive.

If both phases share the same pool of workers, one phase may block the other.

## Prefill Workers

Prefill workers process prompts and prepare state for generation. They may be optimized for high prompt throughput.

## Decode Workers

Decode workers generate output tokens. They may be optimized for long-running token generation and KV cache residency.

## Complexity

Disaggregation adds operational complexity. Systems must move state between workers, schedule requests carefully, and handle failures across phases.

It is usually a later-stage optimization for high-scale systems.

## Key Ideas

- Disaggregation separates inference phases or responsibilities.
- Prefill and decode can scale differently.
- It may improve utilization at high scale.
- It increases system complexity.

## Developer Checklist

- First measure whether prefill or decode is the bottleneck.
- Keep simpler architecture until scale requires separation.
- Track queue time per phase.
- Test failure handling between phases.

