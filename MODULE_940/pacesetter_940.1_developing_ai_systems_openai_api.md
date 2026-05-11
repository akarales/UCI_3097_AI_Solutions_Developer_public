# Pacesetter Guide 940.1 - Developing AI Systems with the OpenAI API

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This section moves beyond single API calls into building complete AI systems. You will learn to design multi-step workflows, implement function calling, manage conversation state, and build applications that combine multiple OpenAI capabilities into coherent systems.

## Learning Objectives

- Design multi-step AI workflows using the OpenAI API
- Implement function calling to let models interact with external tools
- Build conversational systems with state management
- Handle streaming responses for real-time user experiences
- Apply system design patterns for AI applications

---

## Key Concepts

### Function Calling

Function calling lets the model decide when and how to call your Python functions:

```python
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get the current weather for a location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {"type": "string", "description": "City name"},
                    "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]}
                },
                "required": ["location"]
            }
        }
    }
]

response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "What's the weather in NYC?"}],
    tools=tools,
    tool_choice="auto"
)

# Model returns a tool_call with arguments to pass to your function
tool_call = response.choices[0].message.tool_calls[0]
```

### Streaming Responses

```python
stream = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "Explain RAG in detail."}],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

### AI System Design Patterns

| Pattern | Description | Example |
|---------|-------------|---------|
| **Router** | Route requests to different handlers | Classify intent, then call appropriate chain |
| **Pipeline** | Sequential processing steps | Extract -> Validate -> Transform -> Store |
| **Fallback** | Try primary, fall back to secondary | GPT-4o -> GPT-4o-mini -> cached response |
| **Orchestrator** | Central controller managing sub-tasks | Agent that delegates to specialized tools |

---

## Supplementary Resources

### Articles
- [Elink 940.1.1 - Building Applications with GitHub Copilot Agent Mode](https://perscholas.instructure.com/courses/3227/pages/elink-940-dot-1-1-building-applications-with-github-copilot-agent-mode)

---

## DataCamp Course

**[Developing AI Systems with the OpenAI API](https://app.datacamp.com/learn/courses/developing-ai-systems-with-the-openai-api)**

---

## Related Assessment

- **[POC 940.1.1 - Developing AI Systems with the OpenAI API (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627662)**

---

## Canvas Links

- [Pacesetter Guide 940.1](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-940-dot-1-developing-ai-systems-with-the-openai-api)

---

## Questions?
