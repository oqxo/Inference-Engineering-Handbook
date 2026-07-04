# 01. What Is Artificial Intelligence?

Artificial intelligence, or AI, is software that performs tasks that normally require human judgment. Examples include reading text, answering questions, recognizing images, translating languages, writing code, and summarizing documents.

AI is not magic. It is still software. The difference is that traditional software usually follows rules written directly by developers, while AI software learns patterns from data.

In normal programming, a developer writes instructions like:

```text
if the user clicks this button, open this page
```

In AI, the system is often given many examples and learns a pattern. Instead of writing every rule by hand, developers train or use a model that can make predictions.

## What Is A Model?

A model is a program that has learned patterns from data. When you send input to the model, it returns output.

For example:

- Input: "Translate hello to Spanish"
- Output: "hola"

The model does not search a database of every possible answer. It computes an answer using numbers learned during training.

## Why Developers Should Care

AI systems are becoming part of normal software products. A developer may need to add document search, chat support, code generation, image understanding, or speech features.

To do that well, you need to understand more than the API call. You need to understand latency, cost, failure modes, context length, output quality, rate limits, and security.

That is where inference engineering begins.

## Key Ideas

- AI means software that performs tasks involving judgment or pattern recognition.
- A model is the learned part of an AI system.
- Training creates or improves a model.
- Inference uses a trained model to answer requests.
- Production AI is still production software.

## Developer Checklist

- Treat AI output as computed output, not guaranteed truth.
- Measure behavior with real examples.
- Plan for latency, cost, and failures from the start.
- Keep humans in the loop for high-risk decisions.

