# Pacesetter Guide 938.5 - Working with Llama 3

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Llama 3 is Meta's open-source language model family. Working with open-source models gives you flexibility, cost savings, and the ability to run models on your own infrastructure. This section teaches you how to integrate Llama 3 into your applications.

## Learning Objectives

- Understand the Llama model family and its variants
- Run Llama 3 locally using Ollama
- Integrate Llama 3 with Python applications
- Compare Llama 3 with proprietary models (GPT-4, Claude)
- Understand open-source model licensing and use cases

---

## Key Concepts

### Llama 3 Model Variants

| Model | Parameters | Context | Best For |
|-------|-----------|---------|----------|
| **Llama 3 8B** | 8 billion | 128K | Fast local inference, simple tasks |
| **Llama 3 70B** | 70 billion | 128K | High quality, complex reasoning |
| **Llama 3.1 405B** | 405 billion | 128K | Near GPT-4 quality (cloud only) |

### Running Llama 3 with Ollama

```bash
# Install Ollama (https://ollama.com)
# Pull the model
ollama pull llama3

# Run interactively
ollama run llama3

# Run as API server (default port 11434)
ollama serve
```

### Python Integration

```python
# Using the requests library
import requests

response = requests.post('http://localhost:11434/api/chat', json={
    'model': 'llama3',
    'messages': [
        {'role': 'system', 'content': 'You are a helpful assistant.'},
        {'role': 'user', 'content': 'Explain recursion in Python.'}
    ],
    'stream': False
})

print(response.json()['message']['content'])
```

```python
# Using LangChain
from langchain_community.llms import Ollama

llm = Ollama(model="llama3")
response = llm.invoke("What is the difference between a list and a tuple in Python?")
print(response)
```

### Open-Source vs. Proprietary Trade-offs

| Factor | Open-Source (Llama) | Proprietary (GPT-4) |
|--------|-------------------|---------------------|
| **Cost** | Free (compute only) | Pay per token |
| **Privacy** | Data stays local | Data sent to cloud |
| **Quality** | Good, improving fast | Best available |
| **Customization** | Full fine-tuning possible | Limited to prompting |
| **Speed** | Depends on hardware | Optimized infrastructure |
| **Ease of Setup** | Requires local setup | API key and go |

---

## DataCamp Course

**[Working with Llama 3](https://app.datacamp.com/learn/courses/working-with-llama-3)**

---

## Related Assessment

- **[POC 938.5.1 - Working with Llama 3 (16.6 pts)](https://perscholas.instructure.com/courses/3227/assignments/627656)**

---

## Canvas Links

- [Pacesetter Guide 938.5](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-938-dot-5-working-with-llama-3)
