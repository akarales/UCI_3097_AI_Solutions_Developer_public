# Python 3.14 — Conventions & Style Reference

> Based on [PEP 8](https://peps.python.org/pep-0008/), [PEP 257](https://peps.python.org/pep-0257/), and Python 3.14 release changes (October 7, 2025).

---

## Table of Contents

1. [Naming Conventions](#1-naming-conventions)
2. [Indentation & Line Length](#2-indentation--line-length)
3. [Blank Lines & Whitespace](#3-blank-lines--whitespace)
4. [Comments & Docstrings](#4-comments--docstrings)
5. [Type Annotations (Python 3.14 Lazy Evaluation)](#5-type-annotations-python-314-lazy-evaluation)
6. [T-Strings (Python 3.14)](#6-t-strings-python-314)
7. [Imports](#7-imports)
8. [Expressions & Operators](#8-expressions--operators)
9. [Exception Handling](#9-exception-handling)
10. [Access Control & Underscore Patterns](#10-access-control--underscore-patterns)
11. [Tooling](#11-tooling)
12. [Quick Reference Cheat Sheet](#12-quick-reference-cheat-sheet)

---

## 1. Naming Conventions

Python uses different casing styles depending on the kind of identifier. Note that Python does **not** use camelCase for variables or functions — that is a common mistake from developers coming from JavaScript or Java.

### 1.1 Variables — `snake_case`

```python
# CORRECT
user_name = "Alex"
total_count = 42
is_authenticated = True
max_retry_attempts = 3

# WRONG — camelCase is not Python convention
userName = "Alex"
totalCount = 42
isAuthenticated = True
```

### 1.2 Functions — `snake_case`

```python
# CORRECT
def calculate_total_price(base_price: float, tax_rate: float) -> float:
    return base_price * (1 + tax_rate)


def get_user_by_id(user_id: int) -> dict:
    ...


def is_valid_token(token: str) -> bool:
    ...


# WRONG
def CalculateTotalPrice(basePrice, taxRate):  # PascalCase + camelCase — both wrong
    ...
```

### 1.3 Classes — `PascalCase` (also called UpperCamelCase)

```python
# CORRECT
class UserAccount:
    ...


class HttpRequestHandler:
    ...


class AIModelConfig:
    ...


# WRONG
class user_account:    # snake_case — wrong for classes
    ...

class userAccount:     # camelCase — wrong for classes
    ...
```

### 1.4 Constants — `UPPER_SNAKE_CASE`

```python
# CORRECT
MAX_CONNECTIONS = 100
DEFAULT_TIMEOUT = 30
API_BASE_URL = "https://api.example.com"
BLOCK_SIZE_BYTES = 4096

# WRONG
maxConnections = 100   # camelCase
MaxConnections = 100   # PascalCase
```

### 1.5 Modules & Packages — `lowercase` (short, no underscores preferred)

```python
# Module filenames
mymodule.py         # CORRECT
data_utils.py       # CORRECT — underscores acceptable when needed
MyModule.py         # WRONG — no PascalCase
myModule.py         # WRONG — no camelCase
```

```python
# Package (directory) names
import mypackage         # CORRECT
import data_utils        # CORRECT
import MyPackage         # WRONG
```

### 1.6 Exceptions — `PascalCase` with `Error` suffix

```python
# CORRECT
class DatabaseConnectionError(Exception):
    ...


class InvalidTokenError(ValueError):
    ...


class RateLimitExceeded(RuntimeError):  # non-error flow control — no suffix needed
    ...


# WRONG
class database_connection_error(Exception):
    ...
```

### 1.7 Type Variables — `PascalCase` (single letters or short descriptive names)

```python
from typing import TypeVar

T = TypeVar("T")
KT = TypeVar("KT")  # Key Type
VT = TypeVar("VT")  # Value Type

# Descriptive names for complex generics
UserType = TypeVar("UserType", bound="BaseUser")
```

### 1.8 Characters to Avoid in Names

```python
# NEVER use these as single-character variable names:
# l  — looks like 1 (one)
# O  — looks like 0 (zero)
# I  — looks like l (el) or 1

# BAD
l = 10
O = "object"
I = 5

# GOOD
line_count = 10
obj = "object"
index = 5
```

---

## 2. Indentation & Line Length

### 2.1 Always Use 4 Spaces (Never Tabs)

```python
def process_data(data: list) -> list:
    results = []
    for item in data:
        if item > 0:
            results.append(item * 2)
    return results
```

### 2.2 Continuation Lines

```python
# Aligned with opening delimiter
result = some_function(argument_one,
                       argument_two,
                       argument_three)

# OR hanging indent (4 more spaces, closing bracket on its own line)
result = some_function(
    argument_one,
    argument_two,
    argument_three,
)

# Long if-conditions — use extra indentation to distinguish from body
if (
        condition_one
        and condition_two
        and condition_three
):
    do_something()
```

### 2.3 Maximum Line Length

```python
# Aim for 79 characters per line (hard limit: 99 in many modern projects)

# Long string — use implicit concatenation inside parentheses
message = (
    "This is a very long message that would exceed the line limit "
    "if written on a single line."
)

# Long binary operation — break BEFORE the operator
total = (
    first_value
    + second_value
    - third_value
    * fourth_value
)
```

---

## 3. Blank Lines & Whitespace

### 3.1 Blank Lines

```python
import os
import sys


# Two blank lines before top-level functions and classes
def top_level_function():
    pass


def another_top_level_function():
    pass


class MyClass:
    # One blank line between methods inside a class
    def first_method(self):
        pass

    def second_method(self):
        pass

    def third_method(self):
        # Blank lines inside a function to separate logical sections
        data = load_data()
        data = clean_data(data)

        result = process(data)
        return result
```

### 3.2 Whitespace in Expressions

```python
# CORRECT — no spaces inside brackets/parentheses
x = my_list[0]
y = my_dict["key"]
z = (1 + 2) * 3

# CORRECT — one space around assignment and operators
x = 5
result = x + y * z

# CORRECT — no space before colon in slices
my_list[1:10]
my_list[::2]
my_list[1:10:2]

# CORRECT — no extra spaces around keyword argument defaults
def my_function(arg1, arg2=10, arg3="default"):
    ...

# WRONG
x = my_list[ 0 ]
y = my_dict ["key"]
def bad_func(arg = 10):
    ...
```

---

## 4. Comments & Docstrings

### 4.1 Block Comments

```python
# This is a block comment explaining a section of code.
# It starts with a # and a single space.
# It is at the same indentation level as the code it describes.

def authenticate_user(token: str) -> bool:
    # Validate token format before querying the database
    if not token.startswith("Bearer "):
        return False

    # Strip the Bearer prefix and check expiry
    raw_token = token[7:]
    return check_token_validity(raw_token)
```

### 4.2 Inline Comments (use sparingly)

```python
x = x + 1        # Compensate for the border offset
MAX_RETRIES = 5   # Defined by the upstream API contract

# WRONG — stating the obvious
x = x + 1        # Increment x by 1
```

### 4.3 Docstrings (PEP 257)

```python
def fetch_user_profile(user_id: int) -> dict:
    """Fetch a user's profile from the database by ID."""
    ...


def compute_similarity_score(
    text_a: str,
    text_b: str,
    method: str = "cosine",
) -> float:
    """
    Compute the similarity score between two text strings.

    Args:
        text_a: First input string.
        text_b: Second input string.
        method: Similarity algorithm to use ('cosine' or 'jaccard').

    Returns:
        A float between 0.0 and 1.0 representing similarity.

    Raises:
        ValueError: If an unsupported method is specified.
    """
    ...


class DataPipeline:
    """
    Orchestrates an ETL pipeline for processing raw event data.

    Attributes:
        source: The data source connection string.
        batch_size: Number of records processed per batch.
    """

    def __init__(self, source: str, batch_size: int = 1000) -> None:
        """Initialize the pipeline with a source and batch size."""
        self.source = source
        self.batch_size = batch_size
```

---

## 5. Type Annotations (Python 3.14 Lazy Evaluation)

Python 3.14 introduces **deferred (lazy) annotation evaluation** via PEP 649 and PEP 749. Annotations are no longer evaluated at definition time — only when explicitly requested by a tool or at runtime.

### 5.1 What Changed in 3.14

```python
# Python 3.13 and earlier — this would raise NameError
# because Tree isn't fully defined when the hint is evaluated
class Tree:
    def add_child(self, child: Tree) -> None:  # NameError in < 3.14
        ...

# Python 3.14 — works natively, no quotes needed
class Tree:
    def add_child(self, child: Tree) -> None:  # CORRECT in 3.14+
        self.children.append(child)
```

```python
# Previously required workaround (no longer needed in 3.14)
from __future__ import annotations   # Not needed in 3.14+

class Node:
    def connect(self, other: "Node") -> None:  # Quotes no longer required
        ...

# Python 3.14 — clean, no quotes
class Node:
    def connect(self, other: Node) -> None:
        ...
```

### 5.2 Inspecting Annotations with `annotationlib`

```python
import annotationlib

def greet(name: str) -> str:
    return f"Hello, {name}"

# Get annotations as evaluated values (default behavior)
annotations = annotationlib.get_annotations(greet, format=annotationlib.Format.VALUE)
print(annotations)  # {'name': <class 'str'>, 'return': <class 'str'>}

# Get annotations as strings (useful for serialization)
str_annotations = annotationlib.get_annotations(greet, format=annotationlib.Format.STRING)
print(str_annotations)  # {'name': 'str', 'return': 'str'}

# FORWARDREF format — undefined names become ForwardRef markers instead of raising
fwd_annotations = annotationlib.get_annotations(greet, format=annotationlib.Format.FORWARDREF)
```

### 5.3 Common Type Annotation Patterns

```python
from typing import Optional, Union, Any
from collections.abc import Callable, Sequence, Mapping

# Basic types
name: str = "Alex"
count: int = 0
ratio: float = 0.95
active: bool = True

# Optional (can be None)
user_id: Optional[int] = None
# Modern syntax (Python 3.10+)
user_id: int | None = None

# Union of types
result: Union[str, int] = "ok"
result: str | int = "ok"  # Modern syntax

# Collections
names: list[str] = ["Alice", "Bob"]
scores: dict[str, float] = {"Alice": 99.5}
coords: tuple[float, float] = (1.0, 2.0)
unique_ids: set[int] = {1, 2, 3}

# Callables
handler: Callable[[str, int], bool]

# Functions with return types
def build_index(records: Sequence[dict]) -> Mapping[str, list]:
    ...

# Class methods
class APIClient:
    base_url: str
    timeout: int

    def get(self, endpoint: str, params: dict | None = None) -> dict:
        ...

    @classmethod
    def from_env(cls) -> "APIClient":  # Self-reference — quotes still work, or use Self
        ...

# Python 3.11+ Self type
from typing import Self

class Builder:
    def set_name(self, name: str) -> Self:
        self.name = name
        return self
```

### 5.4 TypedDict, Protocol, dataclass

```python
from typing import TypedDict, Protocol
from dataclasses import dataclass, field


class UserRecord(TypedDict):
    id: int
    username: str
    email: str
    is_active: bool


class Serializable(Protocol):
    def to_json(self) -> str:
        ...


@dataclass
class ModelConfig:
    model_name: str
    temperature: float = 0.7
    max_tokens: int = 1024
    stop_sequences: list[str] = field(default_factory=list)
```

---

## 6. T-Strings (Python 3.14)

Python 3.14 introduces **template strings** (`t""`) via PEP 750. Unlike f-strings which immediately produce a string, t-strings return a `Template` object that captures both static parts and interpolated values — enabling safer custom processing.

```python
# f-string — evaluates immediately to a str
name = "World"
greeting = f"Hello, {name}!"
print(type(greeting))   # <class 'str'>
print(greeting)         # Hello, World!

# t-string — returns a Template object
from string.templatelib import Template

template = t"Hello, {name}!"
print(type(template))   # <class 'string.templatelib.Template'>

# Process the Template manually (for escaping, sanitization, etc.)
def render_safe(tmpl: Template) -> str:
    parts = []
    for part in tmpl:
        if isinstance(part, str):
            parts.append(part)
        else:
            # Apply custom escaping to interpolated values
            parts.append(str(part.value).replace("<", "&lt;").replace(">", "&gt;"))
    return "".join(parts)

user_input = "<script>alert('xss')</script>"
safe_output = render_safe(t"User said: {user_input}")
print(safe_output)  # User said: &lt;script&gt;alert('xss')&lt;/script&gt;
```

**Use t-strings when:**
- Generating SQL queries (to prevent injection)
- Rendering HTML/XML safely
- Building structured log messages
- Any context where interpolated values need validation before being embedded

---

## 7. Imports

### 7.1 Import Order (PEP 8)

Imports must be grouped in this order, separated by blank lines:

1. Standard library imports
2. Related third-party imports
3. Local application / library imports

```python
# 1. Standard library
import os
import sys
from pathlib import Path
from typing import Optional

# 2. Third-party
import numpy as np
import pandas as pd
from fastapi import FastAPI, HTTPException

# 3. Local
from myapp.models import User
from myapp.utils import hash_password
```

### 7.2 Import Style

```python
# CORRECT — explicit imports
from os.path import join, exists
from collections import defaultdict, OrderedDict

# AVOID — wildcard imports pollute the namespace
from os import *          # BAD
from mymodule import *    # BAD

# CORRECT — alias only when there is a strong convention
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# WRONG — aliasing without reason
import os as operating_system   # Unnecessary, confusing
```

---

## 8. Expressions & Operators

### 8.1 Comparisons

```python
# CORRECT — use 'is' / 'is not' for None, True, False
if result is None:
    ...

if result is not None:
    ...

if flag is True:
    ...

# WRONG — using == for None/True/False
if result == None:    # Bad
    ...

if result != None:    # Bad
    ...

# CORRECT — checking for empty containers
if my_list:           # Truthy check
    ...

if not my_dict:       # Empty check
    ...

# WRONG
if len(my_list) > 0:  # Verbose
    ...

if my_list == []:     # Verbose
    ...
```

### 8.2 Boolean Expressions

```python
# CORRECT
def is_eligible(age: int, has_id: bool) -> bool:
    return age >= 18 and has_id


# CORRECT — avoid returning True/False explicitly in simple checks
def is_positive(n: int) -> bool:
    return n > 0

# WRONG
def is_positive_bad(n: int) -> bool:
    if n > 0:
        return True
    else:
        return False
```

### 8.3 Walrus Operator (`:=`) — Python 3.8+

```python
# Assign and test in one expression
import re

data = "Error code: 404"

if match := re.search(r"code: (\d+)", data):
    print(f"Found code: {match.group(1)}")

# Useful in while loops
while chunk := file.read(8192):
    process(chunk)
```

---

## 9. Exception Handling

```python
# CORRECT — catch specific exceptions
try:
    result = risky_operation()
except ValueError as e:
    handle_value_error(e)
except (TypeError, KeyError) as e:
    handle_type_or_key_error(e)

# WRONG — bare except catches everything including SystemExit, KeyboardInterrupt
try:
    result = risky_operation()
except:          # BAD
    pass

# WRONG — catching Exception is too broad in most cases
try:
    result = risky_operation()
except Exception:   # Acceptable only at top-level boundaries
    pass

# CORRECT — exception chaining
try:
    connect_to_db()
except OSError as e:
    raise DatabaseConnectionError("Could not connect") from e

# CORRECT — suppress original traceback intentionally
try:
    value = my_dict["key"]
except KeyError as e:
    raise AttributeError(f"Missing attribute: {e}") from None

# CORRECT — custom exception classes
class TokenExpiredError(ValueError):
    """Raised when an authentication token has expired."""

    def __init__(self, token_id: str) -> None:
        self.token_id = token_id
        super().__init__(f"Token {token_id!r} has expired")
```

---

## 10. Access Control & Underscore Patterns

```python
class BlockchainNode:

    # Public — part of the API contract
    node_id: str
    peers: list[str]

    # Single underscore — internal use, not part of public API
    _connection_pool: list
    _retry_count: int

    def _connect(self) -> None:
        """Internal method — not intended for external callers."""
        ...

    # Double underscore — name-mangled to avoid subclass conflicts
    __private_key: bytes

    def __sign(self, data: bytes) -> bytes:
        """Name-mangled to _BlockchainNode__sign in subclasses."""
        ...

    # Dunder methods — implement Python protocols, never invent new ones
    def __repr__(self) -> str:
        return f"BlockchainNode(node_id={self.node_id!r})"

    def __len__(self) -> int:
        return len(self.peers)

    def __eq__(self, other: object) -> bool:
        if not isinstance(other, BlockchainNode):
            return NotImplemented
        return self.node_id == other.node_id


# Avoid conflicts with Python keywords using trailing underscore
class_ = "AdvancedML"   # 'class' is reserved, use 'class_'
type_ = "regression"    # 'type' is a builtin, use 'type_'
id_ = 42                # 'id' is a builtin, use 'id_'

# Throwaway variable — single underscore
for _ in range(10):
    do_something()

_, middle, _ = ("first", "middle", "last")
```

---

## 11. Tooling

Enforce PEP 8 automatically — don't rely on memory alone.

| Tool | Purpose | Command |
|------|---------|---------|
| **Ruff** | Fast linter + formatter (recommended) | `ruff check . && ruff format .` |
| **Black** | Opinionated auto-formatter | `black .` |
| **isort** | Import sorting | `isort .` |
| **mypy** | Static type checker | `mypy src/` |
| **Pylint** | Deep linting + style | `pylint mymodule.py` |
| **Flake8** | Lightweight style checker | `flake8 .` |
| **pyright** | Fast type checker (used by Pyrefly) | `pyright .` |

### Recommended `pyproject.toml` Setup

```toml
[tool.ruff]
line-length = 88
target-version = "py314"

[tool.ruff.lint]
select = ["E", "F", "I", "N", "UP", "ANN"]
ignore = ["ANN101"]

[tool.black]
line-length = 88
target-version = ["py314"]

[tool.mypy]
python_version = "3.14"
strict = true
```

---

## 12. Quick Reference Cheat Sheet

| Identifier Type | Convention | Example |
|----------------|-----------|---------|
| Variable | `snake_case` | `user_name`, `total_count` |
| Function | `snake_case` | `get_user()`, `calculate_tax()` |
| Class | `PascalCase` | `UserAccount`, `HttpClient` |
| Exception | `PascalCase` + `Error` | `DatabaseError`, `TokenExpiredError` |
| Constant | `UPPER_SNAKE_CASE` | `MAX_RETRIES`, `API_KEY` |
| Module | `lowercase` | `utils.py`, `data_loader.py` |
| Package | `lowercase` | `mypackage/`, `aitools/` |
| Type Variable | `PascalCase` | `T`, `KT`, `UserType` |
| Private attr | `_single_leading` | `_cache`, `_pool` |
| Name-mangled | `__double_leading` | `__secret`, `__key` |
| Keyword avoid | `trailing_` | `class_`, `type_`, `id_` |
| Dunder | `__double_both__` | `__init__`, `__repr__` |
| Throwaway | `_` | `for _ in range(n)` |

### Python 3.14 Highlights

| Feature | Before 3.14 | Python 3.14 |
|---------|------------|-------------|
| Forward references | Required quotes: `"ClassName"` | No quotes needed |
| `from __future__ import annotations` | Required for lazy eval | No longer needed |
| Template strings | Only f-strings | `t""` — returns `Template` object |
| Annotation inspection | `typing.get_type_hints()` | `annotationlib.get_annotations()` |
| Parallel execution | Limited by GIL | Subinterpreters + no-GIL build |

---

*Reference: [PEP 8](https://peps.python.org/pep-0008/) | [PEP 257](https://peps.python.org/pep-0257/) | [Python 3.14 What's New](https://docs.python.org/3/whatsnew/3.14.html) | [typing docs](https://docs.python.org/3/library/typing.html) | Released October 7, 2025*
