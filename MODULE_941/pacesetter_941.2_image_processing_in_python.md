# Pacesetter Guide 941.2 - Image Processing in Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

Before feeding images to AI models, you often need to load, resize, crop, filter, and transform them. This section covers Python image processing with libraries like Pillow and OpenCV, which are essential for building multimodal AI pipelines.

## Learning Objectives

- Load, display, and save images using Pillow (PIL)
- Resize, crop, rotate, and transform images
- Apply filters and enhancements
- Convert between color spaces and formats
- Prepare images for AI model input

---

## Key Concepts

### Pillow (PIL) Basics

```python
from PIL import Image, ImageFilter, ImageEnhance

# Load and inspect
img = Image.open("photo.jpg")
print(f"Size: {img.size}, Mode: {img.mode}, Format: {img.format}")

# Resize
img_resized = img.resize((800, 600))

# Crop (left, upper, right, lower)
img_cropped = img.crop((100, 100, 500, 400))

# Rotate
img_rotated = img.rotate(45, expand=True)

# Apply filters
img_blurred = img.filter(ImageFilter.GaussianBlur(radius=5))
img_edges = img.filter(ImageFilter.FIND_EDGES)

# Enhance
enhancer = ImageEnhance.Contrast(img)
img_enhanced = enhancer.enhance(1.5)  # 50% more contrast

# Save
img_resized.save("output.png")
```

### Image Preparation for AI

```python
import base64
from io import BytesIO

def prepare_image_for_api(image_path, max_size=1024):
    """Resize and encode an image for API submission."""
    img = Image.open(image_path)
    
    # Resize if too large
    if max(img.size) > max_size:
        img.thumbnail((max_size, max_size))
    
    # Convert to base64
    buffer = BytesIO()
    img.save(buffer, format="JPEG", quality=85)
    return base64.b64encode(buffer.getvalue()).decode("utf-8")
```

### Common Image Formats

| Format | Best For | Transparency | Compression |
|--------|----------|-------------|-------------|
| **JPEG** | Photos | No | Lossy |
| **PNG** | Screenshots, graphics | Yes | Lossless |
| **WebP** | Web images | Yes | Both |
| **TIFF** | High-quality archives | Yes | Lossless |

---

## DataCamp Course

**[Image Processing in Python](https://app.datacamp.com/learn/courses/image-processing-in-python)**

---

## Related Assessment

- **[POC 941.2.1 - Image Processing in Python (33 pts)](https://perscholas.instructure.com/courses/3227/assignments/627666)**

---

## Canvas Links

- [Pacesetter Guide 941.2](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-941-dot-2-image-processing-in-python)

---

## Questions?
