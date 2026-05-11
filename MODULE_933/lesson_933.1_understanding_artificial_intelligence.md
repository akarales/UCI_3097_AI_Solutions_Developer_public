# Lesson 933.1 - Understanding Artificial Intelligence

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

This lesson introduces the fundamentals of artificial intelligence, covering the history of AI, the evolution from RNNs to Transformers, and modern LLM architectures. You will complete a DataCamp course to build foundational understanding.

## Learning Objectives

- Define artificial intelligence and distinguish between AI, machine learning, and deep learning
- Understand the evolution from RNNs to Transformers
- Describe the Transformer architecture and its key innovations
- Explain how modern LLMs like GPT-4 work at a high level

---

## Section 1: What is Artificial Intelligence?

Artificial Intelligence (AI) is the simulation of human intelligence in machines. AI systems perform tasks that typically require human intelligence: learning, decision-making, pattern recognition, and language understanding.

### The AI Landscape

- **Machine Learning (ML)** - Algorithms that learn from data to make predictions or decisions
- **Deep Learning** - ML using neural networks with many layers
- **Natural Language Processing (NLP)** - Understanding and generating human language
- **Computer Vision** - Enabling machines to interpret visual information
- **Generative AI** - Creating new content such as text, images, and code

---

## Section 2: From RNNs to Transformers

### Before 2017: The Sequential Bottleneck

Before Transformers, AI used Recurrent Neural Networks (RNNs) for language processing:

- **Sequential Processing** - Had to process text word-by-word in order
- **Information Loss** - Context from early words got lost in long sequences
- **Slow Training** - Could not parallelize, each word waited for the previous one
- **Vanishing Gradients** - Long sequences caused numerical instability

### 2017: The Transformer Revolution

The paper "Attention Is All You Need" (Vaswani et al., 2017) changed everything by eliminating sequential processing entirely.

**Key Innovations:**

1. **Self-Attention Mechanism** - Every word attends to every other word simultaneously
2. **Multi-Head Attention** - Multiple attention perspectives running in parallel (original: 8 heads, GPT-4: ~128 heads per layer)
3. **Positional Encoding** - Position information added explicitly using sine/cosine functions
4. **Parallel Processing** - All words processed simultaneously, enabling massive scaling

### Architecture Comparison

| Architecture | Processing | Strengths | Limitations |
|-------------|-----------|-----------|-------------|
| **RNN** | Sequential, one word at a time | Good for simple sequences | Information loss, slow |
| **RNN + Attention** | Sequential with attention | Better long-range capture | Still sequential bottleneck |
| **Transformer** | Parallel attention-based | Massive parallelization, scales to billions | Requires large datasets and compute |

---

## Section 3: Modern LLM Landscape

The Transformer architecture is the foundation of every major AI model:

| Model | Organization | Key Feature |
|-------|-------------|-------------|
| **GPT-4** | OpenAI | Mixture of Experts, 128K context window |
| **Claude** | Anthropic | Strong reasoning, 200K context window |
| **LLaMA** | Meta | Open-source, locally runnable |
| **Gemini** | Google | Multimodal from the ground up |
| **Mistral** | Mistral AI | Efficient open-source models |
| **BERT** | Google | Bidirectional encoding for NLU tasks |

### Why This Matters for You

Understanding Transformers helps you:
- Write more efficient prompts
- Manage context windows effectively
- Estimate computational costs
- Debug model behavior
- Design better AI applications

---

## DataCamp Course

Complete the following DataCamp course to reinforce these concepts:

**[Understanding Artificial Intelligence](https://app.datacamp.com/learn/courses/understanding-artificial-intelligence)**

This course covers AI fundamentals, machine learning concepts, neural networks, and the practical applications of AI in industry.

---

## Additional Resources

- ["Attention Is All You Need" (2017)](https://arxiv.org/abs/1706.03762) - Original Transformer paper
- [GPT-4 Technical Report](https://arxiv.org/abs/2303.08774) - Official report (limited architecture details)
- "The Illustrated Transformer" by Jay Alammar - Excellent visual explanation

---

## Knowledge Check

1. What is the key difference between an RNN and a Transformer?
2. What problem does the self-attention mechanism solve?
3. Why is parallel processing important for training large models?
4. Name three models built on the Transformer architecture.

---

## Canvas Links

- [Lesson 933.1 - Understanding Artificial Intelligence](https://perscholas.instructure.com/courses/3227/pages/lesson-933-dot-1-understanding-artificial-intelligence)

---

## Questions?
