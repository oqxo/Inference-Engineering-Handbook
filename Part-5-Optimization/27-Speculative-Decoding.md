# 27. Speculative Decoding

Speculative decoding is a technique for generating tokens faster.

The basic idea is to use a smaller or cheaper model to guess several tokens, then use the larger model to verify them.

## Why It Can Help

LLM decoding is slow because tokens are normally generated one at a time. If a draft model guesses tokens that the main model accepts, the system can produce multiple tokens with fewer expensive steps.

## Draft Model

The draft model must be faster than the main model. It does not need to be perfect, but its guesses must be accepted often enough to help.

If the draft model is too inaccurate, speculative decoding may add overhead instead of improving speed.

## Verification

The main model verifies whether the guessed tokens are acceptable. This keeps output aligned with the main model while reducing some decode work.

## Tradeoffs

Speculative decoding adds system complexity:

- More model artifacts
- More memory use
- More scheduling complexity
- More tuning

It is useful only when the speedup is worth that complexity.

## Key Ideas

- Speculative decoding uses a fast draft model.
- The main model verifies guessed tokens.
- It can improve decode speed.
- It must be benchmarked for each workload.

## Developer Checklist

- Measure accepted tokens per draft.
- Compare total latency and GPU memory use.
- Test with real prompts and output lengths.
- Avoid adding it before simpler optimizations are measured.

