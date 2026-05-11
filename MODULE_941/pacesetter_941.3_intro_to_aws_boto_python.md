# Pacesetter Guide 941.3 - Introduction to AWS Boto in Python

Version 1.0, May 2026
Created by Alexandros Karales

---

## Overview

AWS Boto3 is the Python SDK for Amazon Web Services. In multimodal AI applications, you need cloud storage for images, documents, and model artifacts. This section teaches you to work with AWS S3 for file storage, which is essential for production AI deployments.

## Learning Objectives

- Set up AWS credentials and configure Boto3
- Create and manage S3 buckets
- Upload, download, and list objects in S3
- Generate pre-signed URLs for temporary access
- Integrate S3 with AI pipelines for image and document storage

---

## Key Concepts

### Boto3 Setup

```python
import boto3

# Create S3 client (reads credentials from environment or ~/.aws/credentials)
s3 = boto3.client('s3')

# Or create with explicit credentials (not recommended for production)
s3 = boto3.client(
    's3',
    aws_access_key_id='YOUR_KEY',
    aws_secret_access_key='YOUR_SECRET',
    region_name='us-east-1'
)
```

### S3 Operations

```python
# Upload a file
s3.upload_file('local_file.jpg', 'my-bucket', 'images/photo.jpg')

# Download a file
s3.download_file('my-bucket', 'images/photo.jpg', 'downloaded.jpg')

# List objects
response = s3.list_objects_v2(Bucket='my-bucket', Prefix='images/')
for obj in response.get('Contents', []):
    print(f"{obj['Key']} - {obj['Size']} bytes")

# Generate pre-signed URL (temporary access, 1 hour)
url = s3.generate_presigned_url(
    'get_object',
    Params={'Bucket': 'my-bucket', 'Key': 'images/photo.jpg'},
    ExpiresIn=3600
)
```

### AI Pipeline Integration

| Step | AWS Service | Purpose |
|------|------------|---------|
| **Store images** | S3 | Upload user images for processing |
| **Store embeddings** | S3 | Persist vector data as files |
| **Store models** | S3 | Model artifact storage |
| **Serve files** | S3 + CloudFront | Deliver processed results |
| **Trigger processing** | S3 Events + Lambda | Auto-process on upload |

---

## DataCamp Course

**[Introduction to AWS Boto in Python](https://app.datacamp.com/learn/courses/introduction-to-aws-boto-in-python)**

---

## Related Assessment

- **[POC 941.3.1 - Introduction to AWS Boto in Python (33 pts)](https://perscholas.instructure.com/courses/3227/assignments/627667)**

---

## Canvas Links

- [Pacesetter Guide 941.3](https://perscholas.instructure.com/courses/3227/pages/pacesetter-guide-941-dot-3-introduction-to-aws-boto-in-python)
