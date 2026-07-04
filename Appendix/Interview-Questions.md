# Interview Questions

## Beginner

1. What is the difference between training and inference?
2. What is a token?
3. Why does a longer prompt usually cost more?
4. What is time to first token?
5. Why can an LLM return different answers to the same prompt?

## Intermediate

1. What are prefill and decode?
2. Why does KV cache use GPU memory?
3. What metrics would you track for an LLM service?
4. How would you benchmark a model server?
5. What are the risks of quantization?

## Production

1. How would you debug high p99 latency in an inference service?
2. What autoscaling signals are useful for LLM serving?
3. How would you roll out a new model safely?
4. How would you reduce inference cost without hurting quality?
5. What should be logged, and what should not be logged, for privacy?

## Practical Exercise

Design a chat service that uses an LLM to answer questions from company documents.

Explain:

- How documents are retrieved.
- How prompts are built.
- Which metrics are collected.
- How output is validated.
- How the system scales.
- How cost is controlled.

