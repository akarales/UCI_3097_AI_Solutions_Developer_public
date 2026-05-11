# CAP 942 - Capstone: AI Project Guidelines

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

The Capstone Project is your opportunity to demonstrate everything you have learned in this course. You will design, build, and present a complete AI application that showcases your skills across the full technology stack. This project is worth **300 points (20% of your final grade)** and serves as a portfolio piece for your job search.

---

## Project Requirements

### Technical Requirements

Your capstone must incorporate **at least 3** of the following components:

| Component | Description | Modules |
|-----------|-------------|---------|
| **LLM Integration** | Use OpenAI API or local models for text generation | 937, 938 |
| **Prompt Engineering** | Well-designed system prompts and user interactions | 938 |
| **RAG Pipeline** | Retrieval-Augmented Generation from a knowledge base | 939 |
| **Vector Database** | Embeddings stored and queried in Pinecone or ChromaDB | 939 |
| **AI Agent** | Autonomous agent with tool use and reasoning | 940 |
| **Multimodal** | Image analysis, document processing, or visual AI | 941 |
| **Cloud Storage** | AWS S3 or similar for file management | 941 |
| **Function Calling** | LLM-driven tool and function execution | 940 |

### Minimum Technical Stack

- Python 3.10+
- At least one LLM API (OpenAI, Ollama, or Hugging Face)
- LangChain for orchestration
- A user interface (CLI, Streamlit, Gradio, or web app)
- Git/GitHub for version control
- A README.md with setup instructions

---

## Deliverables

### 1. Working Application
- Fully functional AI application
- Clean, well-organized code with comments
- Requirements file (`requirements.txt` or `pyproject.toml`)
- Setup instructions in README

### 2. GitHub Repository
- Public or private repository (instructor must have access)
- Meaningful commit history (not a single commit)
- Proper `.gitignore` (no API keys, no virtual environments)
- Professional README with:
  - Project description
  - Features list
  - Tech stack
  - Setup instructions
  - Screenshots or demo video
  - Architecture diagram (recommended)

### 3. Presentation
- 10-15 minute presentation to the class
- Live demo of the application
- Explain your architecture and design decisions
- Discuss challenges faced and how you solved them
- Q&A session

### 4. Documentation
- Architecture overview
- API documentation (if applicable)
- Known limitations and future improvements

---

## Timeline

| Phase | Duration | Activities |
|-------|----------|------------|
| **Planning** | Week 11, Day 1-2 | Choose topic, define scope, create architecture |
| **Development** | Week 11, Day 3 to Week 12, Day 3 | Build the application iteratively |
| **Testing** | Week 12, Day 3-4 | Test, fix bugs, polish UI |
| **Presentation** | Week 12, Day 5 | Present to class |

---

## Grading Rubric

| Criteria | Points | Description |
|----------|--------|-------------|
| **Technical Complexity** | 75 | Depth and breadth of AI features |
| **Code Quality** | 50 | Clean, documented, well-structured code |
| **Functionality** | 50 | Application works as intended |
| **User Experience** | 25 | Interface is usable and intuitive |
| **Documentation** | 25 | README, setup instructions, architecture |
| **Presentation** | 50 | Clear explanation, live demo, Q&A |
| **Creativity** | 25 | Originality and innovation |
| **TOTAL** | **300** | |

---

## Project Ideas

Here are some ideas to get you started (you are not limited to these):

- **AI-Powered Resume Analyzer** - Upload a resume, get feedback and suggestions using RAG
- **Document Q&A System** - Upload PDFs and ask questions using RAG + vector search
- **AI Study Buddy** - Conversational tutor that uses course materials as knowledge base
- **Code Review Agent** - Agent that reviews Python code and suggests improvements
- **Multimodal Receipt Scanner** - Photograph receipts, extract data, categorize expenses
- **AI Customer Support Bot** - Agent with tool access to a product database
- **Content Generator** - Generate blog posts, social media content with different styles
- **Data Analysis Assistant** - Natural language queries against a SQL database
- **AI Meeting Summarizer** - Process meeting recordings/notes and generate action items
- **Portfolio Website Generator** - AI that builds a portfolio site from your resume data

---

## Tips for Success

1. **Start simple, then iterate** - Get a basic version working first, then add features
2. **Use version control from day one** - Commit early and often
3. **Test as you build** - Do not wait until the end to test
4. **Ask for help** - Instructor and TAs are here to support you
5. **Focus on the demo** - A working demo is more impressive than incomplete features
6. **Document as you go** - Write your README while building, not after
7. **Mind your API costs** - Use `gpt-4o-mini` for development, switch to `gpt-4o` for the demo

---

## Submission

Upload your final project to Canvas:

- **[CAP 942 - Capstone - AI Project Guidelines](https://perscholas.instructure.com/courses/3227/assignments/627624)**

Include:
- Link to your GitHub repository
- Any additional documentation

---

## Canvas Links

- [CAP 942 - Capstone Submission](https://perscholas.instructure.com/courses/3227/assignments/627624)
