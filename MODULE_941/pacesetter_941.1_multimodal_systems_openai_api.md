# Pacesetter Guide 941.1 - Multi-Modal Systems with the OpenAI API

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Multimodal AI systems can process and generate multiple types of data: text, images, audio, and video. GPT-4 Vision and other multimodal models enable applications that understand images, generate visual descriptions, and combine visual and textual reasoning.

## Learning Objectives

- Understand multimodal AI and its applications
- Use GPT-4 Vision to analyze and describe images
- Build applications that combine text and image inputs
- Process documents, screenshots, and visual data with AI
- Handle image encoding and API formatting for multimodal requests

---

## Key Concepts

### GPT-4 Vision (Image Analysis)

```python
from openai import OpenAI
import base64

client = OpenAI()

# Method 1: Image URL
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{
        "role": "user",
        "content": [
            {"type": "text", "text": "Describe this image in detail."},
            {"type": "image_url", "image_url": {"url": "https://example.com/image.jpg"\}\}
        ]
    }]
)

# Method 2: Base64 encoded local image
with open("photo.jpg", "rb") as f:
    image_data = base64.b64encode(f.read()).decode("utf-8")

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{
        "role": "user",
        "content": [
            {"type": "text", "text": "What objects are in this image?"},
            {"type": "image_url", "image_url": {
                "url": f"data:image/jpeg;base64,{image_data}"
            }}
        ]
    }]
)
```

### Multimodal Use Cases

| Use Case | Input | Output | Example |
|----------|-------|--------|---------|
| **Image Description** | Image | Text | Accessibility alt-text generation |
| **Document OCR** | Scanned document | Structured text | Invoice data extraction |
| **Visual QA** | Image + Question | Answer | "How many people are in this photo?" |
| **Chart Analysis** | Chart/graph image | Data insights | Analyze sales charts |
| **Code from Screenshot** | UI screenshot | Code | Generate HTML from a mockup |

### Cost Considerations

Image tokens are calculated based on image resolution:
- **Low detail**: Fixed 85 tokens per image
- **High detail**: 85 tokens + 170 tokens per 512x512 tile

---

## DataCamp Course

**[Multi-Modal Systems with the OpenAI API](https://app.datacamp.com/learn/courses/multi-modal-systems-with-the-openai-api)**

---

## Related Assessment

- **[POC 941.1.1 - Multi-Modal Systems with the OpenAI API (33 pts)](https://perscholas.instructure.com/courses/3227/assignments/627665)**

---

## Canvas Links

- [Pacesetter Guide 941.1](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-941-dot-1-multi-modal-systems-with-the-openai-api)

---

## Questions?
