# Pacesetter Guide 937.3 - Working with Hugging Face

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Hugging Face is the open-source hub for AI models, with thousands of models available for free. This section teaches you how to navigate the Hugging Face ecosystem, load pre-trained models, run inference, and integrate models into your Python applications.

## Learning Objectives

- Navigate the Hugging Face Hub to find models and datasets
- Load and use pre-trained models via the Transformers library
- Run inference with pipelines for text generation, classification, and more
- Understand model cards, licensing, and choosing the right model
- Integrate Hugging Face models with LangChain

---

## Key Concepts

### The Hugging Face Ecosystem

| Component | Description | URL |
|-----------|-------------|-----|
| **Hub** | Repository of 500K+ models, datasets, and spaces | [huggingface.co](https://huggingface.co/) |
| **Transformers** | Python library for loading and running models | `pip install transformers` |
| **Datasets** | Library for loading and processing datasets | `pip install datasets` |
| **Spaces** | Platform for hosting ML demo apps | [huggingface.co/spaces](https://huggingface.co/spaces) |
| **Inference API** | Cloud-based model inference without local setup | Via API or `huggingface_hub` |

### Using Pipelines (Simplest Approach)

```python
from transformers import pipeline

# Text generation
generator = pipeline('text-generation', model='gpt2')
result = generator("The future of AI is", max_length=50)
print(result[0]['generated_text'])

# Sentiment analysis
classifier = pipeline('sentiment-analysis')
result = classifier("I really enjoyed this course!")
print(result)  # [{'label': 'POSITIVE', 'score': 0.9998}]

# Summarization
summarizer = pipeline('summarization')
result = summarizer("Long article text here...", max_length=100)
print(result[0]['summary_text'])
```

### Available Pipeline Tasks

| Task | Description | Example Model |
|------|-------------|---------------|
| `text-generation` | Generate text continuations | GPT-2, LLaMA |
| `text-classification` | Classify text (sentiment, etc.) | BERT, DistilBERT |
| `summarization` | Summarize long text | BART, T5 |
| `translation` | Translate between languages | Helsinki-NLP models |
| `question-answering` | Answer questions from context | BERT, RoBERTa |
| `fill-mask` | Predict masked words | BERT |
| `zero-shot-classification` | Classify without training examples | BART-MNLI |

### Choosing a Model

When selecting a model from the Hub, consider:
- **Task** - What are you trying to do?
- **Size** - Larger models are more capable but slower and need more resources
- **License** - Check if the license allows your use case (commercial vs. research)
- **Downloads/Likes** - Popular models are generally more reliable
- **Model Card** - Read the documentation for capabilities and limitations

---

## DataCamp Course

Complete the following DataCamp course:

**[Working with Hugging Face](https://app.datacamp.com/learn/courses/working-with-hugging-face)**

This course covers:
- Navigating the Hugging Face Hub
- Using the Transformers library
- Loading pre-trained models
- Running inference with pipelines
- Fine-tuning basics

---

## Supplementary Resources

### Articles
- [Elink 937.3.1 - Using LangChain with Ollama and Python](https://perscholas.instructure.com/courses/3227/pages/elink-937-dot-3-1-using-langchain-with-ollama-and-python)

### Videos
- [Vlink 937.3.1 - HuggingFace + LangChain: Run 1,000s of Free AI Models Locally](https://perscholas.instructure.com/courses/3227/pages/vlink-937-dot-3-1-huggingface-+-langchain-%7C-run-1-000s-of-free-ai-models-locally)
- [Vlink 937.3.2 - Build an Easy AI App (Python and Hugging Face/LangChain)](https://perscholas.instructure.com/courses/3227/pages/vlink-937-dot-3-2-build-an-easy-ai-app-python-and-hugging-face-slash-langchain)

---

## Related Assessment

- **[POC 937.3.1 - Working with Hugging Face (20 pts)](https://perscholas.instructure.com/courses/3227/assignments/627649)** - Submit your DataCamp badge screenshot

---

## Canvas Links

- [Pacesetter Guide 937.3](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-937-dot-3-working-with-hugging-face)

---

## Questions?
