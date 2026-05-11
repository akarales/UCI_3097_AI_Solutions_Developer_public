# Pacesetter Guide 940.2 - Introduction to AI Agents

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

AI agents are systems that can reason about tasks, make decisions, and take actions autonomously. This is one of the fastest-growing areas in AI. You will learn the ReAct pattern, tool use, planning loops, and how agents differ from simple chatbots.

## Learning Objectives

- Define what makes a system "agentic"
- Understand the ReAct (Reason + Act) pattern
- Build agents that use tools to accomplish goals
- Implement planning and decision-making loops
- Handle agent errors, loops, and safety constraints

---

## Key Concepts

### What Makes a System Agentic?

| Feature | Chatbot | Agent |
|---------|---------|-------|
| **Reasoning** | Responds to prompts | Plans multi-step solutions |
| **Tool Use** | Text only | Calls functions, APIs, databases |
| **Autonomy** | One response per prompt | Multiple actions per goal |
| **State** | Stateless or simple history | Maintains working memory |
| **Decision Making** | None | Chooses which tools to use and when |

### The ReAct Pattern

```
1. OBSERVE  -> Receive the task or new information
2. THINK    -> Reason about what to do next
3. ACT      -> Execute a tool or function
4. OBSERVE  -> See the result
5. REPEAT   -> Until the task is complete
```

### Simple Agent Loop

```python
def agent_loop(task, tools, max_steps=10):
    messages = [
        {"role": "system", "content": "You are a helpful agent with access to tools."},
        {"role": "user", "content": task}
    ]
    
    for step in range(max_steps):
        response = client.chat.completions.create(
            model="gpt-4o",
            messages=messages,
            tools=tools
        )
        
        message = response.choices[0].message
        
        # If no tool calls, the agent is done
        if not message.tool_calls:
            return message.content
        
        # Execute tool calls and add results
        messages.append(message)
        for tool_call in message.tool_calls:
            result = execute_tool(tool_call)
            messages.append({
                "role": "tool",
                "tool_call_id": tool_call.id,
                "content": str(result)
            })
    
    return "Max steps reached."
```

### Agent Safety

- **Max iterations** - Always set a limit on agent loops
- **Tool permissions** - Restrict which tools the agent can call
- **Human-in-the-loop** - Require approval for destructive actions
- **Output validation** - Check agent outputs before acting on them

---

## Supplementary Resources

### Articles
- [Elink 940.2.1 - Introduction to Creating AI Agents in Python](https://perscholas.instructure.com/courses/3227/pages/elink-940-dot-2-1-introduction-to-creating-ai-agents-in-python)

---

## DataCamp Course

**[Introduction to AI Agents](https://app.datacamp.com/learn/courses/introduction-to-ai-agents)**

---

## Related Assessment

- **[POC 940.2.1 - Introduction to AI Agents (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627663)**

---

## Canvas Links

- [Pacesetter Guide 940.2](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-940-dot-2-introduction-to-ai-agents)
