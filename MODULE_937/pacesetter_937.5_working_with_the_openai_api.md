# Pacesetter Guide 937.5 - Working with the OpenAI API

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

The OpenAI API is the industry standard for accessing state-of-the-art language models. This section teaches you how to authenticate, send requests, handle responses, and build applications using the OpenAI Python SDK. This skill translates directly to job requirements.

## Learning Objectives

- Set up and authenticate with the OpenAI API
- Send chat completion requests and handle responses
- Use system, user, and assistant messages effectively
- Understand pricing, token counting, and cost management
- Handle errors, rate limits, and streaming responses

---

## Key Concepts

### Setting Up the OpenAI API

```python
from openai import OpenAI

# Initialize the client (reads OPENAI_API_KEY from environment)
client = OpenAI()

# Or pass the key explicitly (not recommended for production)
client = OpenAI(api_key="sk-...")
```

### Chat Completions

```python
response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": "You are a helpful Python tutor."},
        {"role": "user", "content": "What is a decorator in Python?"}
    ],
    temperature=0.7,
    max_tokens=500
)

print(response.choices[0].message.content)
```

### Message Roles

| Role | Purpose | Example |
|------|---------|---------|
| **system** | Set the model's behavior and persona | "You are a data analysis expert." |
| **user** | The user's input/question | "Analyze this sales data." |
| **assistant** | Previous model responses (for conversation history) | "Based on the data, sales increased by 15%..." |

### Available Models (2025-2026)

| Model | Speed | Cost | Best For |
|-------|-------|------|----------|
| **gpt-4o** | Medium | $$ | Complex reasoning, analysis |
| **gpt-4o-mini** | Fast | $ | General tasks, chat |
| **gpt-4-turbo** | Medium | $$ | Long context (128K) |
| **o1** | Slow | $$$ | Advanced reasoning, math |

### Token Counting and Cost Management

```python
import tiktoken

# Count tokens before sending
encoder = tiktoken.encoding_for_model("gpt-4o-mini")
tokens = encoder.encode("Your prompt text here")
print(f"Token count: {len(tokens)}")

# Check usage after a response
print(f"Prompt tokens: {response.usage.prompt_tokens}")
print(f"Completion tokens: {response.usage.completion_tokens}")
print(f"Total tokens: {response.usage.total_tokens}")
```

### Error Handling

```python
from openai import OpenAI, APIError, RateLimitError, APIConnectionError

client = OpenAI()

try:
    response = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[{"role": "user", "content": "Hello!"}]
    )
except RateLimitError:
    print("Rate limited. Wait and retry.")
except APIConnectionError:
    print("Connection failed. Check your internet.")
except APIError as e:
    print(f"API error: {e}")
```

---

## DataCamp Course

Complete the following DataCamp course:

**[Working with the OpenAI API](https://app.datacamp.com/learn/courses/working-with-the-openai-api)**

This course covers:
- Setting up and authenticating with the OpenAI API
- Chat completions and response handling
- Prompt design and parameter tuning
- Building applications with the API
- Cost management and best practices

---

## Supplementary Resources

### Articles
- [Elink 937.5.1 - A Beginner's Guide to the OpenAI API](https://perscholas.instructure.com/courses/3227/pages/elink-937-dot-5-1-a-beginners-guide-to-the-openai-api)
- [Elink 937.5.2 - Tutorials: OpenAI API](https://perscholas.instructure.com/courses/3227/pages/elink-937-dot-5-2-tutorials-openai-api)

---

## Related Assessment

- **[POC 937.5.1 - Working with the OpenAI API (20 pts)](https://perscholas.instructure.com/courses/3227/assignments/627651)** - Submit your DataCamp badge screenshot

---

## Canvas Links

- [Pacesetter Guide 937.5](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-937-dot-5-working-with-the-openai-api)
