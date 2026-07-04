# 33. Embeddings

An embedding is a vector of numbers that represents meaning.

Embedding models convert text, images, or other data into vectors. Similar items should have vectors that are close to each other.

## Why Embeddings Matter

Embeddings are widely used for search and retrieval.

For example, a user asks:

```text
How do I reset my password?
```

The system can embed the question and search for documents with similar embeddings.

## Vector Search

Vector search finds nearby vectors in a database. This is useful when exact keyword matching is not enough.

The result can be used in retrieval-augmented generation, where relevant documents are added to an LLM prompt.

## Inference Characteristics

Embedding inference is usually different from text generation:

- It produces vectors, not text.
- It is often faster than LLM generation.
- It can be batched efficiently.
- It may run at indexing time and query time.

## Key Ideas

- Embeddings represent meaning as vectors.
- Similar meaning should produce nearby vectors.
- Embeddings power semantic search and retrieval.
- Retrieval quality affects LLM answer quality.

## Developer Checklist

- Use the same embedding model for indexing and querying.
- Rebuild indexes when changing embedding models.
- Evaluate retrieval results before blaming the LLM.
- Store metadata with vectors for filtering and debugging.

