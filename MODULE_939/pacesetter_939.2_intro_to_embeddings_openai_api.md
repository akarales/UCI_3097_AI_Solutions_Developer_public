# Pacesetter Guide 939.2 - Introduction to Embeddings with the OpenAI API

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Embeddings are the mathematical representations that make semantic search possible. This section teaches you how to generate embeddings, understand similarity metrics, and use embeddings for search, clustering, and classification.

## Learning Objectives

- Understand what embeddings are and how they represent meaning
- Generate embeddings using the OpenAI API
- Compute similarity between text using cosine similarity
- Use embeddings for semantic search and document retrieval

---

## Key Concepts

### What Are Embeddings?

Embeddings convert text into numerical vectors where similar meanings map to nearby points in high-dimensional space.

```python
from openai import OpenAI

client = OpenAI()

response = client.embeddings.create(
    model="text-embedding-3-small",
    input="Python is a programming language"
)

vector = response.data[0].embedding  # List of 1536 floats
```

### Cosine Similarity

```python
import numpy as np

def cosine_similarity(a, b):
    return np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))

# Similar texts have similarity close to 1.0
# Unrelated texts have similarity close to 0.0
```

### Embedding Models

| Model | Dimensions | Cost | Best For |
|-------|-----------|------|----------|
| `text-embedding-3-small` | 1536 | $ | Most use cases |
| `text-embedding-3-large` | 3072 | $$ | Higher quality retrieval |
| Hugging Face models | Varies | Free | Local/private deployment |

---

## DataCamp Course

**[Introduction to Embeddings with the OpenAI API](https://app.datacamp.com/learn/courses/introduction-to-embeddings-with-the-openai-api)**

---

## Related Assessment

- **[POC 939.2.1 - Introduction to Embeddings with the OpenAI API (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627659)**

---

## Canvas Links

- [Pacesetter Guide 939.2](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-939-dot-2-introduction-to-embeddings-with-the-openai-api)
