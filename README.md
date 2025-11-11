# Enhancor API Documentation

Official API documentation for Enhancor AI - Portrait and Image Enhancement API

## Available APIs

- **[Realistic Skin Enhancement API](#realistic-skin-enhancement-api)** - Advanced portrait enhancement with skin refinement
- **[Portrait Upscaler API](IMAGE_UPSCALER.md)** - Portrait upscaling with facial feature optimization (Fast/Professional modes)
- **[General Image Upscaler API](GENERAL_UPSCALER.md)** - Universal image upscaling for all image types

---

## Realistic Skin Enhancement API

### Table of Contents

- [Authentication](#authentication)
- [Base URL](#base-url)
- [Endpoints](#endpoints)
  - [Queue Image Processing](#queue-image-processing)
  - [Check Request Status](#check-request-status)
- [Status Codes](#status-codes)
- [Webhook Notifications](#webhook-notifications)
- [Parameters](#parameters)
  - [Enhancement Parameters](#enhancement-parameters)
  - [Area Control Parameters](#area-control-parameters)
  - [Required Parameters](#required-parameters)

## Authentication

All API requests must include your API key in the `x-api-key` header:

```
x-api-key: your_api_key_here
```

## Base URL

```
https://apireq.enhancor.ai/api/realistic-skin/v1
```

## Endpoints

### Queue Image Processing

**POST** `/queue`

Queue an image for processing with specified enhancement parameters.

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

### Enhancement Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `model_version` | string | `"enhancorv1"` | Model version: `"enhancorv1"` or `"enhancorv3"` |
| `enhancementMode` | string | `"standard"` | Enhancement intensity: `"standard"` or `"heavy"` (only for v1) |
| `enhancementType` | string | `"face"` | Enhancement type: `"face"` or `"body"` |
| `skin_refinement_level` | number | `0` | Skin texture enhancement level (0-100) |
| `skin_realism_Level` | number | `1.7` (v1) / `0.1` (v3) | Skin realism level (0-5 for v1, 0-3 for v3) |
| `portrait_depth` | number | `0.2` | Portrait depth (0.2-0.4, only for v3 or v1 heavy mode) |
| `output_resolution` | number | `2048` | Output resolution (1024-3072, only for v3) |
| `mask_image_url` | string | `""` | URL of mask image (only for v3) |
| `mask_expand` | number | `15` | Mask expansion amount (-20 to 20, only for v3) |

### Area Control Parameters

Set to `true` to keep these areas unchanged during processing:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `background` | `false` | Keep background unchanged |
| `skin` | `false` | Keep skin unchanged |
| `nose` | `false` | Keep nose unchanged |
| `eye_g` | `false` | Keep eye area unchanged |
| `r_eye` | `true` | Keep right eye unchanged |
| `l_eye` | `true` | Keep left eye unchanged |
| `r_brow` | `false` | Keep right eyebrow unchanged |
| `l_brow` | `false` | Keep left eyebrow unchanged |
| `r_ear` | `true` | Keep right ear unchanged |
| `l_ear` | `true` | Keep left ear unchanged |
| `mouth` | `true` | Keep mouth unchanged |
| `u_lip` | `true` | Keep upper lip unchanged |
| `l_lip` | `true` | Keep lower lip unchanged |
| `hair` | `false` | Keep hair unchanged |
| `hat` | `false` | Keep hat unchanged |
| `ear_r` | `false` | Keep ear ring unchanged |
| `neck_l` | `false` | Keep necklace unchanged |
| `neck` | `false` | Keep neck unchanged |
| `cloth` | `false` | Keep clothing unchanged |

### Required Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `img_url` | string | **Required** - URL of the image to be processed |
| `webhookUrl` | string | **Required** - URL where the processing result will be sent |

## Example Request

```bash
curl -X POST https://apireq.enhancor.ai/api/realistic-skin/v1/queue \
  -H "Content-Type: application/json" \
  -H "x-api-key: your_api_key_here" \
  -d '{
    "img_url": "https://example.com/image.png",
    "webhookUrl": "https://your-webhook-url.com",
    "model_version": "enhancorv3",
    "enhancementType": "face",
    "skin_refinement_level": 50,
    "output_resolution": 2048
  }'
```

## Support

For support and questions, please contact the Enhancor team.

---

© 2025 Enhancor AI. All rights reserved.
