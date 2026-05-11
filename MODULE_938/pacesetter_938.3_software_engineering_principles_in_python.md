# Pacesetter Guide 938.3 - Software Engineering Principles in Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This section goes beyond scripting into proper software engineering. When your AI application needs to be maintained, scaled, and deployed, solid engineering practices are essential. You will learn about code organization, testing, documentation, and environment management.

## Learning Objectives

- Apply software engineering principles to Python projects
- Structure Python projects with proper modules and packages
- Write tests using pytest
- Manage dependencies with virtual environments and requirements files
- Follow PEP 8 style guidelines and use linting tools

---

## Key Concepts

### Project Structure for AI Applications

```
my_ai_app/
├── src/
│   ├── __init__.py
│   ├── main.py           # Application entry point
│   ├── models/            # LLM interaction code
│   │   ├── __init__.py
│   │   └── openai_client.py
│   ├── prompts/           # Prompt templates
│   │   ├── __init__.py
│   │   └── templates.py
│   └── utils/             # Utility functions
│       ├── __init__.py
│       └── helpers.py
├── tests/
│   ├── test_models.py
│   └── test_prompts.py
├── .env                   # API keys (never commit!)
├── .gitignore
├── requirements.txt
└── README.md
```

### Environment Management

```bash
# Create virtual environment
python -m venv .venv

# Activate it
source .venv/bin/activate  # macOS/Linux
.venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Freeze current dependencies
pip freeze > requirements.txt
```

### Testing with pytest

```python
# tests/test_prompts.py
import pytest
from src.prompts.templates import format_system_prompt

def test_format_system_prompt():
    result = format_system_prompt("Python tutor")
    assert "Python tutor" in result
    assert isinstance(result, str)

def test_format_system_prompt_empty():
    with pytest.raises(ValueError):
        format_system_prompt("")
```

### Security Best Practices

- **Never hardcode API keys** - Use environment variables or `.env` files
- **Add `.env` to `.gitignore`** - Prevent accidental key exposure
- **Use `python-dotenv`** - Load environment variables from `.env` files
- **Rotate keys regularly** - Especially if accidentally exposed

---

## DataCamp Course

**[Software Engineering Principles in Python](https://app.datacamp.com/learn/courses/software-engineering-principles-in-python)**

---

## Related Assessment

- **[POC 938.3.1 - Software Engineering Principles in Python (16.6 pts)](https://perscholas.instructure.com/courses/3227/assignments/627654)**

---

## Canvas Links

- [Pacesetter Guide 938.3](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-938-dot-3-software-engineering-principles-in-python)

---

## Questions?
