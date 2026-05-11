# Pacesetter Guide 939.3 - Vector Databases for Embeddings with Pinecone

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Vector databases are purpose-built for storing and searching embeddings at scale. Pinecone is a leading managed vector database. This section teaches you to create indexes, upsert vectors, query for similar documents, and manage namespaces.

## Learning Objectives

- Understand what vector databases are and why they exist
- Set up and configure Pinecone
- Create indexes, upsert embeddings, and query for similar vectors
- Use namespaces and metadata filtering
- Integrate Pinecone with LangChain for RAG pipelines

---

## Key Concepts

### Vector Database Operations

```python
from pinecone import Pinecone

pc = Pinecone(api_key="YOUR_KEY")

# Create an index
pc.create_index(
    name="my-index",
    dimension=1536,
    metric="cosine"
)

index = pc.Index("my-index")

# Upsert vectors
index.upsert(vectors=[
    {"id": "doc1", "values": [0.1, 0.2, ...], "metadata": {"source": "report.pdf"}},
    {"id": "doc2", "values": [0.3, 0.4, ...], "metadata": {"source": "article.md"}}
])

# Query for similar vectors
results = index.query(vector=[0.1, 0.2, ...], top_k=5, include_metadata=True)
```

### Vector DB Comparison

| Database | Type | Hosting | Best For |
|----------|------|---------|----------|
| **Pinecone** | Managed | Cloud | Production, scaling |
| **ChromaDB** | Open-source | Local/Cloud | Development, prototyping |
| **Weaviate** | Open-source | Self-hosted/Cloud | Complex queries |
| **FAISS** | Library | In-memory | Fast local search |

---

## DataCamp Course

**[Vector Databases for Embeddings with Pinecone](https://app.datacamp.com/learn/courses/vector-databases-for-embeddings-with-pinecone)**

---

## Related Assessment

- **[POC 939.3.1 - Vector Databases for Embeddings with Pinecone (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627660)**

---

## Canvas Links

- [Pacesetter Guide 939.3](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-939-dot-3-vector-databases-for-embeddings-with-pinecone)

---

## Questions?
