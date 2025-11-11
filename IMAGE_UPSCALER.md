# Image Upscaler API

Specialized API for upscaling portrait images with optimized facial features and skin details.

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
https://apireq.enhancor.ai/api/upscaler/v1
```

## Endpoints

### Queue Image Processing

**POST** `/queue`

Queue an image for upscaling with specified processing mode.

**Request Headers:**
```
Content-Type: application/json
x-api-key: your_api_key_here
```

**Request Body:**
```json
{
  "img_url": "https://example.com/image.png",
  "webhookUrl": "https://your-webhook-url.com",
  "mode": "fast"
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

### Processing Mode

| Parameter | Type | Required | Options | Description |
|-----------|------|----------|---------|-------------|
| `mode` | string | **Yes** | `"fast"` or `"professional"` | Processing quality mode |

**Mode Details:**

- **fast**: Quick processing with good quality enhancement
- **professional**: Higher quality processing with enhanced details

### Required Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `img_url` | string | **Required** - URL of the image to be processed |
| `webhookUrl` | string | **Required** - URL where the processing result will be sent |
| `mode` | string | **Required** - Processing mode: `"fast"` or `"professional"` |

## Service Description

**Portrait Upscaler:**

Specialized for portrait images, this service optimizes facial features and skin details while upscaling the image resolution. It provides:

- Enhanced facial feature clarity
- Improved skin texture and details
- Resolution upscaling
- Preservation of natural appearance

## Example Requests

### Fast Mode

```bash
curl -X POST https://apireq.enhancor.ai/api/upscaler/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "img_url": "https://example.com/portrait.jpg",
    "webhookUrl": "https://your-webhook-url.com",
    "mode": "fast"
  }'
```

### Professional Mode

```bash
curl -X POST https://apireq.enhancor.ai/api/upscaler/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "img_url": "https://example.com/portrait.jpg",
    "webhookUrl": "https://your-webhook-url.com",
    "mode": "professional"
  }'
```

### Check Status

```bash
curl -X POST https://apireq.enhancor.ai/api/upscaler/v1/status \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "request_id": "your_request_id"
  }'
```

## Support

For support and questions, please contact the Enhancor team.

---

[← Back to Main Documentation](README.md)

© 2025 Enhancor AI. All rights reserved.
