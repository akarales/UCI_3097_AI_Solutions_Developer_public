# Pacesetter Guide 937.4 - Introduction to LLMs in Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This section brings together the theoretical concepts from 937.2 and the Hugging Face skills from 937.3 into practical Python programming with LLMs. You will learn to interact with language models programmatically, run models locally, and use the LangChain framework.

## Learning Objectives

- Write Python code that interacts with LLMs using various libraries
- Run language models locally using GPT4All and Ollama
- Understand the LangChain framework and its core components
- Build simple LLM-powered applications in Python
- Compare cloud-based vs. local model inference

---

## Key Concepts

### Ways to Access LLMs in Python

| Method | Pros | Cons | Best For |
|--------|------|------|----------|
| **OpenAI API** | Most capable models, easy to use | Costs money, requires internet | Production apps |
| **Hugging Face** | Free models, huge selection | Smaller models, needs GPU for large ones | Research, prototyping |
| **Ollama** | Free, local, private | Limited model selection, needs hardware | Development, privacy |
| **GPT4All** | Free, local, easy setup | Less powerful than cloud models | Learning, offline use |
| **LangChain** | Unified interface, chains/agents | Learning curve, abstraction overhead | Complex applications |

### Running Models Locally with Ollama

```python
# After installing Ollama and pulling a model:
# ollama pull llama3

import requests

response = requests.post('http://localhost:11434/api/generate', json={
    'model': 'llama3',
    'prompt': 'Explain what an API is in simple terms.',
    'stream': False
})

print(response.json()['response'])
```

### LangChain Basics

LangChain is the orchestration framework you'll use throughout this course:

```python
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage, SystemMessage

# Create a chat model instance
chat = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)

# Send messages
messages = [
    SystemMessage(content="You are a helpful Python tutor."),
    HumanMessage(content="Explain list comprehensions with an example.")
]

response = chat.invoke(messages)
print(response.content)
```

### Key LangChain Components

| Component | Purpose | Example |
|-----------|---------|---------|
| **Chat Models** | Interface to LLMs | `ChatOpenAI`, `ChatOllama` |
| **Prompt Templates** | Reusable prompt structures | `ChatPromptTemplate` |
| **Output Parsers** | Parse model output into structured data | `JsonOutputParser` |
| **Chains** | Connect multiple steps together | `prompt | model | parser` |
| **Memory** | Maintain conversation history | `ConversationBufferMemory` |

---

## DataCamp Course

Complete the following DataCamp course:

**[Introduction to LLMs in Python](https://app.datacamp.com/learn/courses/introduction-to-llms-in-python)**

This course covers:
- Working with LLMs programmatically in Python
- Using different model providers
- Prompt design and response handling
- Building simple LLM applications

---

## Supplementary Resources

### Videos
- [Vlink 937.4.1 - Using LLMs in Python](https://perscholas.instructure.com/courses/3227/pages/vlink-937-dot-4-1-using-llms-in-python)
- [Vlink 937.4.2 - How to Run a Large Language Model Locally Using GPT4All](https://perscholas.instructure.com/courses/3227/pages/vlink-937-dot-4-2-how-to-run-a-large-language-model-llm-locally-using-gpt4all)
- [Vlink 937.4.3 - LangChain Explained in 13 Minutes](https://perscholas.instructure.com/courses/3227/pages/vlink-937-dot-4-3-langchain-explained-in-13-minutes-%7C-quickstart-tutorial-for-beginners)

---

## Related Assessment

- **[POC 937.4.1 - Introduction to LLMs in Python (20 pts)](https://perscholas.instructure.com/courses/3227/assignments/627650)** - Submit your DataCamp badge screenshot

---

## Canvas Links

- [Pacesetter Guide 937.4](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-937-dot-4-introduction-to-llms-in-python)
