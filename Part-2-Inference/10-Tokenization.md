# 10. Tokenization

Tokenization converts text into tokens that a model can process.

A model does not read characters exactly like humans do. It reads token IDs. The tokenizer maps text to numbers before inference and maps generated numbers back to text after inference.

## Tokens Are Not Always Words

The sentence:

```text
Inference engineering is useful.
```

may become tokens like:

```text
Inference | engineering | is | useful | .
```

But a rare word may be split into smaller pieces. Spaces and punctuation can also matter.

## Why Token Count Matters

Token count affects:

- Cost
- Latency
- Memory use
- Context window usage
- Maximum output length

Two strings with the same character count may have different token counts.

## Tokenizer Compatibility

Different models may use different tokenizers. If you switch models, token counts and behavior may change.

This matters when you set limits, estimate cost, or build prompts that must fit within a context window.

## Practical Advice

Always measure token counts with the tokenizer for the model you actually use. Character count is only a rough estimate.

For production systems, store useful metrics:

- Prompt tokens
- Generated tokens
- Total tokens
- Tokens per second

## Key Ideas

- Tokenization maps text to model-readable numbers.
- Tokens are not always words.
- Token count affects speed, cost, and memory.
- Different models can tokenize differently.

## Developer Checklist

- Count tokens before sending large prompts.
- Enforce input and output limits.
- Track token usage in logs and metrics.
- Retest prompts when changing models.

