# Pacesetter Guide 939.1 - Retrieval Augmented Generation (RAG) with LangChain

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

RAG is the technique that allows LLMs to answer questions using your own data. Instead of relying on the model's training data, RAG retrieves relevant documents from your knowledge base and includes them in the prompt context. This is one of the most commercially valuable skills in AI development.

## Learning Objectives

- Understand the RAG architecture and pipeline
- Build document loaders and text splitters
- Create embeddings from text chunks
- Store and retrieve vectors from a vector database
- Generate grounded responses with citations

---

## Key Concepts

### The RAG Pipeline

```
1. INGEST     -> Load documents (PDFs, web pages, databases)
2. CHUNK      -> Split documents into smaller pieces
3. EMBED      -> Convert chunks to numerical vectors
4. INDEX      -> Store vectors in a vector database
5. RETRIEVE   -> Find relevant chunks for a query
6. GENERATE   -> Pass context + query to LLM for a grounded answer
```

### Document Loading

```python
from langchain_community.document_loaders import (
    PyPDFLoader, TextLoader, WebBaseLoader
)

# Load a PDF
loader = PyPDFLoader("document.pdf")
docs = loader.load()

# Load from web
loader = WebBaseLoader("https://example.com/article")
docs = loader.load()
```

### Text Splitting

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,      # Characters per chunk
    chunk_overlap=200,    # Overlap between chunks
    separators=["\n\n", "\n", ". ", " "]
)

chunks = splitter.split_documents(docs)
```

### Why RAG Matters

| Without RAG | With RAG |
|-------------|----------|
| Model hallucinates facts | Answers grounded in your data |
| Knowledge cutoff date | Access to current information |
| Generic responses | Specific, cited answers |
| No source attribution | Can cite exact sources |

---

## DataCamp Course

**[Retrieval Augmented Generation (RAG) with LangChain](https://app.datacamp.com/learn/courses/retrieval-augmented-generation-rag-with-langchain)**

---

## Related Assessment

- **[POC 939.1.1 - RAG with LangChain (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627658)**

---

## Canvas Links

- [Pacesetter Guide 939.1](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-939-dot-1-retrieval-augmented-generation-rag-with-langchain)
