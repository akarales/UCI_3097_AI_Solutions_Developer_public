# Pacesetter Guide 938.1 - Understanding Prompt Engineering

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Prompt engineering is the art and science of designing inputs that reliably produce desired outputs from language models. This is arguably the most in-demand AI skill right now, applicable to every LLM interaction you will ever have.

## Learning Objectives

- Understand what prompt engineering is and why it matters
- Apply zero-shot, few-shot, and chain-of-thought prompting techniques
- Design system prompts that control model behavior
- Structure prompts for consistent, reliable outputs
- Recognize and mitigate common prompting pitfalls

---

## Key Concepts

### Prompting Techniques

| Technique | Description | When to Use |
|-----------|-------------|-------------|
| **Zero-shot** | No examples, just instructions | Simple, well-defined tasks |
| **Few-shot** | Include examples of desired input/output pairs | When output format matters |
| **Chain-of-thought** | Ask the model to reason step by step | Complex reasoning, math, logic |
| **Role prompting** | Assign the model a specific persona/role | Domain-specific expertise |
| **Structured output** | Request specific formats (JSON, tables, lists) | Data extraction, APIs |

### Prompt Structure Best Practices

```
[System Message]  - Who the model is, what rules to follow
[Context]          - Background information
[Instruction]      - What you want the model to do
[Input Data]       - The data to process
[Output Format]    - How you want the response formatted
[Examples]         - (Optional) Few-shot examples
```

### Common Pitfalls

- **Vague instructions** - "Make it better" vs. "Rewrite this paragraph to be more concise, using active voice"
- **No output format** - Always specify if you need JSON, bullet points, a table, etc.
- **Too much at once** - Break complex tasks into smaller prompts
- **Ignoring temperature** - Use low temperature (0.0-0.3) for factual tasks, higher (0.7-1.0) for creative tasks

---

## DataCamp Course

**[Understanding Prompt Engineering](https://app.datacamp.com/learn/courses/understanding-prompt-engineering)**

---

## Related Assessment

- **[POC 938.1.1 - Understanding Prompt Engineering (16.6 pts)](https://perscholas.instructure.com/courses/3227/assignments/627652)**

---

## Canvas Links

- [Pacesetter Guide 938.1](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-938-dot-1-understanding-prompt-engineering)
