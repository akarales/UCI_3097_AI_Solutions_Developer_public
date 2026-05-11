# Lesson 938.7 - Install and Run LLMs Locally

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Running LLMs locally is important for development, testing, privacy-sensitive applications, and understanding model performance without cloud costs. This lesson covers installing and using both Ollama and GPT4All on your local machine.

## Learning Objectives

- Install and configure Ollama for local model inference
- Install and configure GPT4All as an alternative local runtime
- Pull and run different model sizes
- Understand hardware requirements for local inference
- Compare Ollama and GPT4All for different use cases

---

## Section 1: Ollama

### Installation

```bash
# Linux
curl -fsSL https://ollama.com/install.sh | sh

# macOS
brew install ollama

# Windows - Download from https://ollama.com
```

### Basic Usage

```bash
# Pull a model
ollama pull llama3
ollama pull mistral
ollama pull codellama

# Run interactively
ollama run llama3

# List installed models
ollama list

# Remove a model
ollama rm llama3
```

### API Server

Ollama runs an API server on `http://localhost:11434`:

```python
import requests

# Chat endpoint
response = requests.post('http://localhost:11434/api/chat', json={
    'model': 'llama3',
    'messages': [{'role': 'user', 'content': 'Hello!'}],
    'stream': False
})
print(response.json()['message']['content'])

# Generate endpoint (simpler)
response = requests.post('http://localhost:11434/api/generate', json={
    'model': 'llama3',
    'prompt': 'Explain Python decorators.',
    'stream': False
})
print(response.json()['response'])
```

### Recommended Models

| Model | Size | Speed | Best For |
|-------|------|-------|----------|
| `llama3:8b` | ~4.7 GB | Fast | General chat, coding |
| `mistral` | ~4.1 GB | Fast | European language support |
| `codellama` | ~3.8 GB | Fast | Code generation |
| `llama3:70b` | ~39 GB | Slow | High-quality responses |
| `phi3` | ~2.3 GB | Very fast | Lightweight tasks |

---

## Section 2: GPT4All

### Installation

```bash
# Python package
pip install gpt4all

# Or download the desktop app from https://gpt4all.io
```

### Python Usage

```python
from gpt4all import GPT4All

# Download and load a model
model = GPT4All("Meta-Llama-3-8B-Instruct.Q4_0.gguf")

# Generate text
output = model.generate("Explain what an API is.", max_tokens=200)
print(output)

# Chat with session context
with model.chat_session():
    response1 = model.generate("What is Python?")
    response2 = model.generate("Give me an example.")  # Remembers context
```

---

## Section 3: Hardware Requirements

| Model Size | RAM Needed | GPU VRAM | Performance |
|-----------|-----------|----------|-------------|
| 3B params | 4 GB | 4 GB | Real-time on most machines |
| 7-8B params | 8 GB | 6 GB | Good on modern laptops |
| 13B params | 16 GB | 10 GB | Needs good hardware |
| 70B params | 48 GB | 40 GB | Needs workstation/server |

### Tips for Limited Hardware
- Use quantized models (Q4_0, Q5_K_M) for smaller file sizes
- Close other applications to free RAM
- Use the smallest model that meets your quality needs
- Consider cloud APIs for tasks that need large models

---

## Related Labs (Ungraded)

- **[GLAB 938.7 - Ollama Installation and Usage Guide](https://perscholas.instructure.com/courses/3227/assignments/627635)**
- **[GLAB 938.8 - GPT4All Local Installation and Usage Guide](https://perscholas.instructure.com/courses/3227/assignments/627636)**

---

## Canvas Links

- [Lesson 938.7 - Install and Run LLMs Locally](https://perscholas.instructure.com/courses/3227/pages/lesson-938-dot-7-install-and-run-llms-locally)

---

## Questions?
