# Kora Pro API

AI-powered image generation API with advanced models for creating high-quality images from text prompts.

## Table of Contents

- [Authentication](#authentication)
- [Base URL](#base-url)
- [Endpoints](#endpoints)
  - [Queue Image Processing](#queue-image-processing)
  - [Check Request Status](#check-request-status)
- [Status Codes](#status-codes)
- [Webhook Notifications](#webhook-notifications)
- [Parameters](#parameters)
  - [Required Parameters](#required-parameters)
  - [Optional Parameters](#optional-parameters)
- [Models](#models)
- [Generation Modes](#generation-modes)
- [Image Sizes](#image-sizes)

## Authentication

All API requests must include your API key in the `x-api-key` header:

```
x-api-key: your_api_key_here
```

## Base URL

```
https://apireq.enhancor.ai/api/kora/v1
```

## Endpoints

### Queue Image Processing

**POST** `/queue`

Queue an image generation request with specified parameters.

**Request Headers:**
```
Content-Type: application/json
x-api-key: your_api_key_here
```

**Request Body:**
```json
{
  "model": "kora_pro",
  "prompt": "A sample prompt",
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
| `model` | string | **Required** - Model to use: `"kora_pro"` or `"kora_pro_cinema"` |
| `prompt` | string | **Required** - Text prompt describing the image to generate |
| `webhookUrl` | string | **Required** - URL where the processing result will be sent |

### Optional Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `img_url` | string | `""` | URL of reference image for image-to-image generation |
| `generation_mode` | string | `"normal"` | Generation quality: `"normal"`, `"2k_pro"`, or `"4k_ultra"` |
| `image_size` | string | `"portrait_3:4"` | Output image dimensions (see [Image Sizes](#image-sizes)) |

## Models

### Available Models

| Model | Description | Best For |
|-------|-------------|----------|
| `kora_pro` | Standard high-quality generation | General purpose image creation |
| `kora_pro_cinema` | Cinematic style generation | Movie-like, dramatic imagery |

## Generation Modes

| Mode | Resolution | Quality | Use Case |
|------|-----------|---------|----------|
| `normal` | Standard | Good | Quick generation, testing |
| `2k_pro` | 2K | High | Professional work |
| `4k_ultra` | 4K | Ultra | Maximum quality, print-ready |

## Image Sizes

### Preset Sizes

| Size Option | Aspect Ratio | Description |
|------------|--------------|-------------|
| `portrait_3:4` | 3:4 | Standard portrait |
| `portrait_9:16` | 9:16 | Mobile/story format |
| `square` | 1:1 | Square format |
| `landscape_4:3` | 4:3 | Standard landscape |
| `landscape_16:9` | 16:9 | Widescreen format |

### Custom Sizes

For custom dimensions, use the format: `custom_WIDTH_HEIGHT`

**Examples:**
- `custom_1024_1024` - 1024x1024 pixels
- `custom_1920_1080` - 1920x1080 pixels
- `custom_2048_1536` - 2048x1536 pixels

## Example Requests

### Basic Text-to-Image Generation

```bash
curl -X POST https://apireq.enhancor.ai/api/kora/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "model": "kora_pro",
    "prompt": "A serene mountain landscape at sunset with vibrant colors",
    "webhookUrl": "https://your-webhook-url.com"
  }'
```

### High-Quality Cinematic Generation

```bash
curl -X POST https://apireq.enhancor.ai/api/kora/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "model": "kora_pro_cinema",
    "prompt": "Epic sci-fi cityscape with neon lights and flying vehicles",
    "generation_mode": "4k_ultra",
    "image_size": "landscape_16:9",
    "webhookUrl": "https://your-webhook-url.com"
  }'
```

### Image-to-Image with Custom Size

```bash
curl -X POST https://apireq.enhancor.ai/api/kora/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "model": "kora_pro",
    "prompt": "Transform into a watercolor painting style",
    "img_url": "https://example.com/reference-image.jpg",
    "generation_mode": "2k_pro",
    "image_size": "custom_2048_1536",
    "webhookUrl": "https://your-webhook-url.com"
  }'
```

### Check Status

```bash
curl -X POST https://apireq.enhancor.ai/api/kora/v1/status \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "request_id": "your_request_id"
  }'
```

## Use Cases

**Kora Pro API is perfect for:**

- **Creative Content**: Generate unique artwork and illustrations
- **Marketing Materials**: Create custom visuals for campaigns
- **Concept Art**: Rapid prototyping of visual ideas
- **Social Media**: Generate engaging visual content
- **Product Visualization**: Create product mockups and concepts
- **Cinematic Content**: Movie-style imagery with kora_pro_cinema
- **Print Materials**: High-resolution outputs with 4k_ultra mode

## Tips for Best Results

1. **Detailed Prompts**: More specific descriptions yield better results
2. **Style Keywords**: Include style descriptors (e.g., "photorealistic", "oil painting", "minimalist")
3. **Quality Mode**: Use `4k_ultra` for final production work
4. **Aspect Ratio**: Choose appropriate size for your use case
5. **Model Selection**: Use `kora_pro_cinema` for dramatic, cinematic effects

## Support

For support and questions, please contact the Enhancor team.

---

[← Back to Main Documentation](README.md)

© 2025 Enhancor AI. All rights reserved.
