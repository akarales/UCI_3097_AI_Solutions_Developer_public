# Lesson 933.4 - Using GitHub Copilot with Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This lesson builds on the Copilot fundamentals by focusing specifically on using GitHub Copilot with Python. You will learn how to leverage Copilot for Python-specific tasks including API integration, data manipulation, and AI application development.

## Learning Objectives

- Use GitHub Copilot effectively with Python code
- Generate Python functions, classes, and test cases using Copilot
- Apply Copilot to common Python tasks: API requests, data processing, file handling
- Understand Python-specific Copilot tips and patterns

---

## Section 1: Copilot with Python

Python is one of the languages where Copilot excels due to the massive amount of Python code in its training data. This makes it especially useful for:

### Common Python Tasks with Copilot

| Task | How to Prompt | Example |
|------|--------------|---------|
| **API Requests** | "Write a function to GET data from an API using requests" | HTTP client functions |
| **Data Processing** | "Parse this JSON response and extract the title field" | JSON/CSV handling |
| **File I/O** | "Read a CSV file and return a list of dictionaries" | File manipulation |
| **Error Handling** | "Add try/except blocks for network errors" | Exception handling |
| **Testing** | "Write pytest tests for this function" | Unit test generation |
| **Documentation** | "Add a docstring to this function" | Code documentation |

### Tips for Python-Specific Prompting

1. **Include type hints** - `def fetch_data(url: str) -> dict:` gives Copilot better context
2. **Write docstrings first** - Describe what the function should do before writing the body
3. **Use descriptive variable names** - `api_response` is better than `r` for Copilot context
4. **Import statements** - Start with your imports to set the context for the file

---

## Section 2: Practical Examples

### Example: Making an API Request

```python
# Write a function that fetches user data from JSONPlaceholder API
# and returns the user's name and email
def get_user_info(user_id: int) -> dict:
    """Fetch user info from JSONPlaceholder API.
    
    Args:
        user_id: The ID of the user to fetch
        
    Returns:
        Dictionary with 'name' and 'email' keys
    """
    # Copilot will suggest the implementation based on this context
```

### Example: Processing JSON Data

```python
# Parse a list of posts and return only posts with more than 50 characters in the title
def filter_long_titles(posts: list[dict]) -> list[dict]:
    """Filter posts to only include those with titles longer than 50 characters."""
    # Copilot suggests: return [post for post in posts if len(post['title']) > 50]
```

---

## Microsoft Learn Course

Complete the following module:

**[Introduction to Copilot with Python](https://learn.microsoft.com/en-us/training/modules/introduction-copilot-python/)**

This module covers:
- Setting up Copilot for Python development
- Writing effective prompts for Python code generation
- Using Copilot for debugging and testing Python code
- Best practices for AI-assisted Python development

---

## Homework: AI Coding Challenge (933.4.1)

After completing the Microsoft Learn module, complete the AI Coding Challenge assignment in Canvas. This is an ungraded homework assignment to practice your skills.

- [933.4.1 - AI Coding Challenge](https://perscholas.instructure.com/courses/3227/assignments/627623)

---

## Knowledge Check

1. Why does Copilot work particularly well with Python?
2. How do type hints improve Copilot's suggestions?
3. Write a comment that would prompt Copilot to generate an API request function.
4. What should you always do before accepting a Copilot suggestion?

---

## Canvas Links

- [Lesson 933.4 - Using GitHub Copilot with Python](https://perscholas.instructure.com/courses/3227/pages/lesson-933-dot-4-using-github-copilot-with-python)
