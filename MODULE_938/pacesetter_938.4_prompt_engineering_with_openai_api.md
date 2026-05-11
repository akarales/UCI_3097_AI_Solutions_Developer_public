# Pacesetter Guide 938.4 - Prompt Engineering with the OpenAI API

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This section combines prompt engineering theory with the OpenAI API. You will design system prompts, manage conversation history, implement structured outputs, and build applications that use prompting strategies programmatically.

## Learning Objectives

- Design effective system prompts for different use cases
- Implement few-shot prompting via the API
- Use structured output formats (JSON mode)
- Manage multi-turn conversations with message history
- Apply chain-of-thought prompting programmatically

---

## Key Concepts

### System Prompt Design Patterns

```python
# Role-based system prompt
system_prompt = """You are a senior Python developer with 10 years of experience.
When reviewing code:
1. Identify bugs and security issues first
2. Suggest improvements with code examples
3. Rate the code quality on a scale of 1-10
4. Always explain your reasoning

Output format: Use markdown with code blocks."""

# Structured output system prompt
system_prompt = """You are a data extraction assistant.
Extract the requested information and return it as valid JSON.
Never include explanations outside the JSON structure.
If information is not found, use null."""
```

### JSON Mode (Structured Output)

```python
response = client.chat.completions.create(
    model="gpt-4o-mini",
    response_format={"type": "json_object"},
    messages=[
        {"role": "system", "content": "Extract entities as JSON with keys: name, type, description"},
        {"role": "user", "content": "OpenAI created GPT-4, a large language model."}
    ]
)

import json
data = json.loads(response.choices[0].message.content)
```

### Multi-turn Conversation Management

```python
conversation_history = [
    {"role": "system", "content": "You are a helpful coding assistant."}
]

def chat(user_message):
    conversation_history.append({"role": "user", "content": user_message})
    
    response = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=conversation_history
    )
    
    assistant_message = response.choices[0].message.content
    conversation_history.append({"role": "assistant", "content": assistant_message})
    
    return assistant_message
```

---

## DataCamp Course

**[Prompt Engineering with the OpenAI API](https://app.datacamp.com/learn/courses/prompt-engineering-with-the-openai-api)**

---

## Related Assessment

- **[POC 938.4.1 - Prompt Engineering with the OpenAI API (16.6 pts)](https://perscholas.instructure.com/courses/3227/assignments/627655)**

---

## Canvas Links

- [Pacesetter Guide 938.4](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-938-dot-4-prompt-engineering-with-the-openai-api)
