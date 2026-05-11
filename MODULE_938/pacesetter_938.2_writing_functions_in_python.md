# Pacesetter Guide 938.2 - Writing Functions in Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Before building complex AI workflows, your Python fundamentals need to be solid. This section reinforces function design, parameter handling, return values, scope, and error handling. Clean, modular code is essential when building multi-step AI pipelines.

## Learning Objectives

- Write well-structured Python functions with proper parameters and return values
- Understand variable scope, closures, and lambda functions
- Apply decorators and higher-order functions
- Handle errors gracefully with try/except
- Write docstrings and type hints for maintainable code

---

## Key Concepts

### Function Design Principles

```python
def analyze_sentiment(text: str, model: str = "gpt-4o-mini") -> dict:
    """Analyze the sentiment of input text using an LLM.
    
    Args:
        text: The text to analyze
        model: The model to use (default: gpt-4o-mini)
        
    Returns:
        Dictionary with 'sentiment' and 'confidence' keys
    """
    # Implementation here
    pass
```

### Key Patterns for AI Development

| Pattern | Description | AI Use Case |
|---------|-------------|-------------|
| **Default parameters** | Sensible defaults for optional args | Default model, temperature |
| **Return dictionaries** | Return structured data | API response handling |
| **Error handling** | Try/except for external calls | API failures, timeouts |
| **Type hints** | Document expected types | Code clarity, IDE support |
| **Decorators** | Wrap functions with extra behavior | Retry logic, logging, caching |

### Decorators for AI Applications

```python
import time
import functools

def retry(max_attempts=3, delay=1):
    """Retry decorator for API calls."""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
                    time.sleep(delay * (attempt + 1))
        return wrapper
    return decorator

@retry(max_attempts=3, delay=2)
def call_openai_api(prompt):
    # API call that might fail
    pass
```

---

## DataCamp Course

**[Writing Functions in Python](https://app.datacamp.com/learn/courses/writing-functions-in-python)**

---

## Related Assessment

- **[POC 938.1.2 - Writing Functions in Python (16.6 pts)](https://perscholas.instructure.com/courses/3227/assignments/627653)**

---

## Canvas Links

- [Pacesetter Guide 938.2](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-938-dot-2-writing-functions-in-python)
