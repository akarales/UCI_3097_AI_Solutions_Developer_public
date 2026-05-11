# Pacesetter Guide 938.6 - Developing LLM Applications with LangChain

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

LangChain is the orchestration framework that ties everything together. This section teaches you to build multi-step applications using chains, prompt templates, output parsers, and memory. LangChain is the framework you will use for RAG, agents, and production AI applications.

## Learning Objectives

- Build LangChain chains that connect prompts, models, and parsers
- Create reusable prompt templates with variables
- Parse model outputs into structured Python objects
- Implement conversation memory for multi-turn applications
- Chain multiple LLM calls together for complex workflows

---

## Key Concepts

### LangChain Expression Language (LCEL)

```python
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# Define the chain using the pipe operator
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a {role}. Respond concisely."),
    ("user", "{question}")
])

model = ChatOpenAI(model="gpt-4o-mini")
parser = StrOutputParser()

chain = prompt | model | parser

# Run the chain
result = chain.invoke({
    "role": "Python expert",
    "question": "What are list comprehensions?"
})
```

### Prompt Templates

```python
from langchain_core.prompts import ChatPromptTemplate

# Simple template
template = ChatPromptTemplate.from_template(
    "Summarize the following text in {num_sentences} sentences:\n\n{text}"
)

# Multi-message template
template = ChatPromptTemplate.from_messages([
    ("system", "You are an expert in {domain}."),
    ("user", "Explain {topic} to a beginner.")
])
```

### Output Parsers

```python
from langchain_core.output_parsers import JsonOutputParser
from pydantic import BaseModel, Field

class SentimentResult(BaseModel):
    sentiment: str = Field(description="positive, negative, or neutral")
    confidence: float = Field(description="confidence score 0.0 to 1.0")
    reasoning: str = Field(description="brief explanation")

parser = JsonOutputParser(pydantic_object=SentimentResult)

# Include format instructions in your prompt
prompt = ChatPromptTemplate.from_messages([
    ("system", "Analyze sentiment. {format_instructions}"),
    ("user", "{text}")
]).partial(format_instructions=parser.get_format_instructions())

chain = prompt | model | parser
```

### Conversation Memory

```python
from langchain_community.chat_message_histories import ChatMessageHistory
from langchain_core.runnables.history import RunnableWithMessageHistory

store = {}

def get_session_history(session_id: str):
    if session_id not in store:
        store[session_id] = ChatMessageHistory()
    return store[session_id]

chain_with_memory = RunnableWithMessageHistory(
    chain,
    get_session_history,
    input_messages_key="question",
    history_messages_key="history"
)
```

---

## DataCamp Course

**[Developing LLM Applications with LangChain](https://app.datacamp.com/learn/courses/developing-llm-applications-with-langchain)**

---

## Related Assessment

- **[POC 938.6.1 - Developing LLM Applications with LangChain (16.6 pts)](https://perscholas.instructure.com/courses/3227/assignments/627657)**

---

## Canvas Links

- [Pacesetter Guide 938.6](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-938-dot-6-developing-llm-applications-with-langchain)
