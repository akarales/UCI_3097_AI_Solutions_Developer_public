# The Complete Python UV Guide - From Setup to Production

---

**Author:** Alexandros Karales (He / Him)  
**Title:** Lead Technical Instructor - Artificial Intelligence & Data Analytics  
**Email:** [akarales@perscholas.org](mailto:akarales@perscholas.org)  
**Organization:** Per Scholas  

---

> A comprehensive guide to managing Python projects with `uv`, the ultra-fast package manager built in Rust by Astral. This guide is intended for students and developers transitioning from `pip` to modern Python tooling.

---

## 1. What is uv?

`uv` is an extremely fast Python package installer and resolver written in Rust by Astral (the creators of Ruff). It is designed as a drop-in replacement for `pip` and `pip-tools`, offering 10–100x faster package installation and dependency resolution. It handles virtual environments, Python version management, dependency locking, and project scaffolding - all in a single tool.

> **Why uv over pip?** When engineers review your GitHub projects, seeing `uv` in your README signals that you are an up-to-date developer who knows current tooling. `pip` is the old way - `uv` is the standard modern Python projects are moving toward.

---

## 2. Installation

### Windows

**PowerShell (Recommended)**
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Using pip**
```powershell
pip install uv
```

**Using pipx**
```powershell
pipx install uv
```

### macOS

**Homebrew (Recommended)**
```bash
brew install uv
```

**curl**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Linux

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Verify Installation

```bash
uv --version
```

### Troubleshooting Installation

**Windows - `uv` not found:**
```powershell
$env:PATH += ";$env:USERPROFILE\.cargo\bin"
```

**macOS/Linux - `uv` not found:**
```bash
source $HOME/.cargo/env
```

---

## 3. Python Version Management

`uv` can install and manage multiple Python versions without needing `pyenv` or similar tools.

```bash
# Install a specific version
uv python install 3.12

# Install multiple versions at once
uv python install 3.11 3.12 3.13

# List all available versions
uv python list

# List only installed versions
uv python list --only-installed

# Find the active Python
uv python find
```

### Pin a Version for Your Project

```bash
uv python pin 3.12
```

This creates a `.python-version` file and ensures everyone working on the project uses the same Python version - critical for team consistency and reproducible environments.

> **Important:** For AI/ML work, use Python 3.10 or 3.11. Python 3.14 is too new - many packages have not caught up yet and will throw errors.

---

## 4. Initializing a Project

### The Correct uv Workflow

```bash
# Step 1 - Initialize the project (creates pyproject.toml)
uv init

# Step 2 - Add your dependencies
uv add <package-name>

# Step 3 - Run your script
uv run your_script.py
```

> **Common mistake:** Running `uv add` before `uv init` will throw `No pyproject.toml found`. Always initialize first.

### Create a New Project in a New Folder

```bash
uv init my-project
cd my-project
```

This scaffolds the following structure:

```
my-project/
├── .python-version
├── .venv/
├── README.md
├── pyproject.toml
└── hello.py
```

### Specify Python Version at Init

```bash
uv init --python 3.11 my-project
```

### Project Types

```bash
# Application (default)
uv init my-app

# Library (creates src/ layout)
uv init --lib my-library
```

---

## 5. Virtual Environment Management

### Automatic (Recommended)

`uv` creates and manages a `.venv` automatically when you run `uv init`. You do **not** need to manually activate it when using `uv run`:

```bash
uv run python script.py
uv run pytest
uv run black .
```

### Manual Activation (When Needed)

```bash
# macOS / Linux
source .venv/bin/activate

# Windows CMD
.venv\Scripts\activate.bat

# Windows PowerShell
.venv\Scripts\Activate.ps1

# Deactivate
deactivate
```

### Recreating a Virtual Environment

```bash
rm -rf .venv
uv init
```

---

## 6. Adding and Managing Dependencies

### Add Packages

```bash
# Single package
uv add requests

# Multiple packages
uv add requests numpy pandas

# Version constraints
uv add "fastapi>=0.100.0"
uv add "django~=4.2"
```

### Development Dependencies

```bash
uv add --dev pytest black ruff
```

### Remove Packages

```bash
uv remove requests
```

### List Installed Packages

```bash
uv pip list

# Show the full dependency tree
uv tree
```

---

## 7. Syncing and Locking Dependencies

```bash
# Install all dependencies from pyproject.toml / lock file
uv sync

# Generate or update the lock file
uv lock

# Upgrade all packages
uv lock --upgrade

# Upgrade a single package
uv lock --upgrade-package requests

# Force reinstall everything
uv sync --reinstall
```

### Working with requirements.txt

```bash
# Compile a requirements.txt from pyproject.toml
uv pip compile pyproject.toml -o requirements.txt

# Install from requirements.txt
uv pip install -r requirements.txt
```

---

## 8. Running Code

```bash
# Run a script using the project environment
uv run your_script.py

# Run a module
uv run -m pytest

# Run a formatter
uv run black .
```

### Standalone Scripts with Inline Dependencies

`uv` supports scripts that declare their own dependencies inline:

```python
# /// script
# requires-python = ">=3.11"
# dependencies = [
#     "requests",
#     "rich",
# ]
# ///

import requests
from rich import print

response = requests.get("https://api.github.com")
print(f"[green]Status: {response.status_code}[/green]")
```

```bash
uv run script.py
# uv creates a temporary environment automatically - no manual install needed
```

---

## 9. Practical Example - GPT4All on macOS

This is a real-world example of how to use `uv` for an AI project on macOS.

```bash
# Navigate to your project folder
cd /Users/yourname/Desktop/PerScholas_AI/module_938

# Initialize the uv project
uv init

# Add gpt4all
uv add gpt4all

# Run your script
uv run gpt4all_test_two.py
```

Your `gpt4all_test_two.py`:

```python
from gpt4all import GPT4All

# Update the path to match your local model location
model = GPT4All("/Users/yourname/Library/Application Support/nomic.ai/GPT4All/meta-llama-3.1-8b-instruct.Q4_0.gguf")

with model.chat_session():
    response = model.generate("Hello, how are you?")
    print(response)
```

> **Troubleshooting:** If you get `No module named 'pkg_resources'`, this is a Python 3.14 compatibility issue. Use `uv init --python 3.11` instead.

---

## 10. Migrating from pip / Other Tools

### From pip

```bash
uv init
uv add $(cat requirements.txt)
```

### From Poetry

```bash
poetry export -f requirements.txt -o requirements.txt
uv init
uv pip install -r requirements.txt
```

### From Pipenv

```bash
pipenv requirements > requirements.txt
uv init
uv add $(cat requirements.txt)
```

---

## 11. Cache Management

```bash
# Show cache location
uv cache dir

# Clear cache
uv cache clean
```

---

## 12. Quick Command Reference

| Command | Description |
|---|---|
| `uv init` | Initialize a new project (creates `pyproject.toml`) |
| `uv init --lib` | Initialize a library project |
| `uv add <pkg>` | Add a dependency |
| `uv add --dev <pkg>` | Add a dev dependency |
| `uv remove <pkg>` | Remove a dependency |
| `uv sync` | Install deps from lock file |
| `uv lock` | Generate / update lock file |
| `uv lock --upgrade` | Upgrade all locked deps |
| `uv run <script>` | Run a script in the project environment |
| `uv venv` | Manually create a virtual environment |
| `uv python install <ver>` | Install a Python version |
| `uv python pin <ver>` | Pin project Python version |
| `uv python list` | List available Python versions |
| `uv pip list` | List installed packages |
| `uv tree` | Show full dependency tree |
| `uv cache clean` | Clear the cache |
| `deactivate` | Deactivate an active venv |

---

## 13. Best Practices

1. **Always run `uv init` before `uv add`** - `pyproject.toml` must exist first.
2. **Prefer `uv run` over activating venvs** - faster and eliminates the "forgot to activate" mistake.
3. **Commit `uv.lock`** - ensures reproducible builds across machines and CI pipelines.
4. **Use `pyproject.toml` as your source of truth** - avoid `requirements.txt` as the primary dependency file.
5. **Pin your Python version** - use `.python-version` so the whole team stays consistent.
6. **Stick to Python 3.10 or 3.11 for AI/ML work** - newer versions (3.13+) may not be supported by packages yet.
7. **Organize deps into groups** - separate dev, test, lint, and production dependencies.
8. **Run `uv lock --upgrade` periodically** - keep dependencies current.
9. **Use `uv cache clean` when things break** - resolves most obscure resolution issues.
10. **Document `uv` in your README** - it shows collaborators and potential employers you use modern tooling.

---

## 14. Further Reading

- Official Documentation: [docs.astral.sh/uv](https://docs.astral.sh/uv/)
- Astral GitHub: [github.com/astral-sh/uv](https://github.com/astral-sh/uv)

---

*Prepared by Alexandros Karales - Per Scholas AI & Data Analytics Program*  
*[akarales@perscholas.org](mailto:akarales@perscholas.org)*
