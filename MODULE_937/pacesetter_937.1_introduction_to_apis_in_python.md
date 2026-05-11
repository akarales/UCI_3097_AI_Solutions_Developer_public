# Pacesetter Guide 937.1 - Introduction to APIs in Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This section introduces Application Programming Interfaces (APIs) and how to work with them using Python. APIs are the foundation of modern AI development, as every AI service (OpenAI, Hugging Face, etc.) is accessed through APIs.

## Learning Objectives

- Understand what APIs are and how they enable software communication
- Make HTTP requests using Python's `requests` library
- Work with JSON data returned from API endpoints
- Handle API authentication, status codes, and error responses
- Build Python functions that integrate with external APIs

---

## Key Concepts

### What is an API?

An API is like a waiter at a restaurant: you (the client) make a request, the waiter (API) delivers it to the kitchen (server), and brings back the response. APIs define the rules for how software components communicate.

### HTTP Methods

| Method | Purpose | Example |
|--------|---------|---------|
| **GET** | Retrieve data | Get a list of users |
| **POST** | Send/create data | Submit a new record |
| **PUT** | Update data | Modify an existing record |
| **DELETE** | Remove data | Delete a record |

### Status Codes

| Code | Meaning | Action |
|------|---------|--------|
| **200** | Success | Process the response |
| **201** | Created | Resource was created |
| **400** | Bad Request | Check your request parameters |
| **401** | Unauthorized | Check your API key |
| **404** | Not Found | Check the endpoint URL |
| **429** | Rate Limited | Wait and retry |
| **500** | Server Error | Not your fault, retry later |

### JSON (JavaScript Object Notation)

JSON is the standard data format for API responses. In Python, JSON maps directly to dictionaries and lists:

```python
import requests

response = requests.get('https://jsonplaceholder.typicode.com/posts/1')
data = response.json()  # Converts JSON to Python dict

print(data['title'])   # Access fields like a dictionary
print(data['userId'])  # Nested data works the same way
```

### API Authentication

Most production APIs require authentication:

```python
import requests

headers = {
    'Authorization': 'Bearer YOUR_API_KEY',
    'Content-Type': 'application/json'
}

response = requests.get('https://api.example.com/data', headers=headers)
```

---

## DataCamp Course

Complete the following DataCamp course:

**[Introduction to APIs in Python](https://app.datacamp.com/learn/courses/introduction-to-apis-in-python)**

This course covers:
- Making HTTP requests with the `requests` library
- Working with REST APIs
- Parsing JSON responses
- Handling authentication and errors
- Building API integrations

---

## Supplementary Resources

### Articles
- [Elink 937.1.2 - Python REST APIs with Flask, Connexion, and SQLAlchemy](https://perscholas.instructure.com/courses/3227/pages/elink-937-dot-1-2-python-rest-apis-with-flask-connexion-and-sqlalchemy) - Learn how to build your own REST API

---

## Related Assessment

- **[POC 937.1.1 - Introduction to APIs in Python (20 pts)](https://perscholas.instructure.com/courses/3227/assignments/627647)** - Submit your DataCamp badge screenshot

---

## Canvas Links

- [Pacesetter Guide 937.1](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-937-dot-1-introduction-to-apis-in-python)

---

## Questions?
