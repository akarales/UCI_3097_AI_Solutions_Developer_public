# Pacesetter Guide 940.3 - Designing Agentic Systems with LangChain

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

LangChain provides a powerful framework for building agentic systems with built-in tool management, memory, and orchestration. This section teaches you to build production-ready agents using LangChain's agent framework.

## Learning Objectives

- Build LangChain agents with custom tools
- Implement different agent types (ReAct, structured chat)
- Add memory and conversation history to agents
- Create multi-tool agents that can search, calculate, and query data
- Debug and trace agent execution

---

## Key Concepts

### LangChain Agent Architecture

```python
from langchain_openai import ChatOpenAI
from langchain.agents import AgentExecutor, create_react_agent
from langchain_core.tools import tool
from langchain import hub

@tool
def search_database(query: str) -> str:
    """Search the product database for information."""
    # Your database search logic here
    return f"Results for: {query}"

@tool
def calculate(expression: str) -> str:
    """Evaluate a mathematical expression."""
    return str(eval(expression))

# Create the agent
llm = ChatOpenAI(model="gpt-4o-mini")
prompt = hub.pull("hwchase17/react")
tools = [search_database, calculate]

agent = create_react_agent(llm, tools, prompt)
executor = AgentExecutor(agent=agent, tools=tools, verbose=True)

result = executor.invoke({"input": "What is the price of item X and how much is 10% off?"})
```

### Custom Tools

```python
from langchain_core.tools import tool
from pydantic import BaseModel, Field

class WeatherInput(BaseModel):
    city: str = Field(description="The city to get weather for")
    unit: str = Field(default="celsius", description="Temperature unit")

@tool(args_schema=WeatherInput)
def get_weather(city: str, unit: str = "celsius") -> str:
    """Get the current weather for a city."""
    # API call here
    return f"Weather in {city}: 22 degrees {unit}"
```

### Agent Debugging

```python
# Enable verbose mode to see agent reasoning
executor = AgentExecutor(
    agent=agent,
    tools=tools,
    verbose=True,        # Print reasoning steps
    max_iterations=10,   # Prevent infinite loops
    handle_parsing_errors=True  # Graceful error handling
)
```

---

## DataCamp Course

**[Designing Agentic Systems with LangChain](https://app.datacamp.com/learn/courses/designing-agentic-systems-with-langchain)**

---

## Related Assessment

- **[POC 940.3.1 - Designing Agentic Systems with LangChain (25 pts)](https://perscholas.instructure.com/courses/3227/assignments/627664)**

---

## Canvas Links

- [Pacesetter Guide 940.3](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-940-dot-3-designing-agentic-systems-with-langchain)

---

## Questions?
