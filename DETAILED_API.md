# Detailed API

Advanced image processing API that combines upscaling with detailed enhancement capabilities. Perfect for professional photography and high-quality image production.

## Table of Contents

- [Authentication](#authentication)
- [Base URL](#base-url)
- [Endpoints](#endpoints)
  - [Queue Image Processing](#queue-image-processing)
  - [Check Request Status](#check-request-status)
- [Status Codes](#status-codes)
- [Webhook Notifications](#webhook-notifications)
- [Parameters](#parameters)
- [Service Description](#service-description)

## Authentication

All API requests must include your API key in the `x-api-key` header:

```
x-api-key: your_api_key_here
```

## Base URL

```
https://apireq.enhancor.ai/api/detailed/v1
```

## Endpoints

### Queue Image Processing

**POST** `/queue`

Queue an image for detailed processing and enhancement.

**Request Headers:**
```
Content-Type: application/json
x-api-key: your_api_key_here
```

**Request Body:**
```json
{
  "img_url": "https://example.com/image.png",
  "webhookUrl": "https://your-webhook-url.com"
}
```

**Response:**
```json
{
  "success": true,
  "requestId": "unique_request_id"
}
```

### Check Request Status

**POST** `/status`

Check the processing status of a queued request.

**Request Headers:**
```
Content-Type: application/json
x-api-key: your_api_key_here
```

**Request Body:**
```json
{
  "request_id": "your_request_id"
}
```

**Response:**
```json
{
  "requestId": "unique_request_id",
  "status": "IN_QUEUE",
  "cost": 480
}
```

## Status Codes

The API returns the following status codes:

| Status | Description |
|--------|-------------|
| `PENDING` | Request is pending processing |
| `IN_QUEUE` | Request is in the processing queue |
| `IN_PROGRESS` | Request is being processed |
| `COMPLETED` | Request has been completed successfully |
| `FAILED` | Request failed to process |

## Webhook Notifications

When a request is completed, the system will send a POST request to your provided webhook URL with the following payload:

```json
{
  "request_id": "unique_request_id",
  "result": "https://example.com/processed-image.png",
  "status": "success"
}
```

## Parameters

### Required Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `img_url` | string | **Required** - URL of the image to be processed |
| `webhookUrl` | string | **Required** - URL where the processing result will be sent |

## Service Description

**Detailed API:**

Advanced image processing API that combines upscaling with detailed enhancement capabilities. This service provides:

- **Combined Processing**: Upscaling + detailed enhancement in one operation
- **Professional Quality**: Optimized for high-quality image production
- **Detail Preservation**: Maintains fine details while enhancing overall quality
- **Advanced Enhancement**: Superior to standard upscaling alone
- **Production Ready**: Perfect for professional photography workflows

**Ideal Use Cases:**

- Professional photography
- Commercial product images
- High-resolution prints
- Marketing materials
- Portfolio work
- Editorial content
- Fine art reproduction

**Key Benefits:**

- Single API call for comprehensive enhancement
- Optimized processing pipeline
- Consistent high-quality results
- Time-efficient workflow
- Professional-grade output

## Example Requests

### Queue Image for Detailed Processing

```bash
curl -X POST https://apireq.enhancor.ai/api/detailed/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "img_url": "https://example.com/professional-photo.jpg",
    "webhookUrl": "https://your-webhook-url.com"
  }'
```

### Check Status

```bash
curl -X POST https://apireq.enhancor.ai/api/detailed/v1/status \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "request_id": "your_request_id"
  }'
```

## API Comparison

| Feature | Detailed API | General Upscaler | Portrait Upscaler |
|---------|-------------|------------------|-------------------|
| **Processing** | Upscaling + Enhancement | Upscaling only | Portrait-specific upscaling |
| **Quality Level** | Professional | Standard | Portrait-optimized |
| **Best For** | Professional work | General images | Portraits only |
| **Detail Enhancement** | Advanced | Standard | Facial features |
| **Use Case** | Commercial/Professional | Everyday images | Headshots/Portraits |

## Support

For support and questions, please contact the Enhancor team.

---

[← Back to Main Documentation](README.md)

© 2025 Enhancor AI. All rights reserved.
