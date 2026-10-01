# Namatube API Contract

This document serves as the **single source of truth** for all REST API endpoints connecting the NamaFront (React frontend) and NamaBackend (Django microservices). All frontend and backend implementations must strictly adhere to this contract.

## General Guidelines

### Base URL
- **Development:** `http://localhost:8000/api/v1`
- **Production:** `https://api.namatube.com/v1`

### Authentication
All authenticated endpoints require a JWT token in the Authorization header:
```
Authorization: Bearer <jwt_token>
```

### Response Format
All responses follow this structure:
```json
{
  "success": true,
  "data": { ... },
  "error": null,
  "timestamp": "2026-10-02T00:00:00Z"
}
```

Error responses:
```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message"
  },
  "timestamp": "2026-10-02T00:00:00Z"
}
```

### HTTP Status Codes
- `200 OK`: Successful request
- `201 Created`: Resource successfully created
- `400 Bad Request`: Invalid request data
- `401 Unauthorized`: Missing or invalid authentication
- `403 Forbidden`: Insufficient permissions
- `404 Not Found`: Resource not found
- `429 Too Many Requests`: Rate limit exceeded
- `500 Internal Server Error`: Server-side error

---

## Authentication Service Endpoints

### POST /auth/register
Register a new user account.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "username": "username"
}
```

**Response (201):**
```json
{
  "success": true,
  "data": {
    "userId": "uuid-here",
    "email": "user@example.com",
    "username": "username"
  }
}
```

### POST /auth/login
Authenticate and receive JWT token.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "token": "jwt.token.here",
    "refreshToken": "refresh.token.here",
    "expiresIn": 3600,
    "user": {
      "userId": "uuid-here",
      "email": "user@example.com",
      "username": "username"
    }
  }
}
```

### POST /auth/logout
Invalidate current session.

**Headers:** `Authorization: Bearer <token>`

**Response (200):**
```json
{
  "success": true,
  "data": {
    "message": "Successfully logged out"
  }
}
```

---

## Video Service Endpoints

### POST /videos/upload
Upload a new video.

**Headers:** `Authorization: Bearer <token>`, `Content-Type: multipart/form-data`

**Request (multipart):**
- `file`: Video file (required)
- `title`: Video title (required)
- `description`: Video description (optional)
- `privacy`: "public" | "unlisted" | "private" (default: "public")
- `category`: Category ID (optional)

**Response (201):**
```json
{
  "success": true,
  "data": {
    "videoId": "uuid-here",
    "status": "processing",
    "title": "Video Title",
    "uploadedAt": "2026-10-02T00:00:00Z"
  }
}
```

### GET /videos/:videoId
Retrieve video metadata and streaming URL.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "videoId": "uuid-here",
    "title": "Video Title",
    "description": "Description here",
    "duration": 120,
    "thumbnailUrl": "https://cdn.namatube.com/thumbnails/...",
    "streamUrl": "https://cdn.namatube.com/videos/...",
    "views": 1500,
    "uploadedAt": "2026-10-02T00:00:00Z",
    "channel": {
      "channelId": "uuid-here",
      "name": "Channel Name"
    }
  }
}
```

### DELETE /videos/:videoId
Delete a video (owner only).

**Headers:** `Authorization: Bearer <token>`

**Response (200):**
```json
{
  "success": true,
  "data": {
    "message": "Video deleted successfully"
  }
}
```

---

## Interaction Service Endpoints

### POST /videos/:videoId/like
Like a video.

**Headers:** `Authorization: Bearer <token>`

**Response (200):**
```json
{
  "success": true,
  "data": {
    "liked": true,
    "likeCount": 150
  }
}
```

### POST /videos/:videoId/comments
Add a comment to a video.

**Headers:** `Authorization: Bearer <token>`

**Request:**
```json
{
  "text": "Great video!",
  "parentId": "optional-parent-comment-id"
}
```

**Response (201):**
```json
{
  "success": true,
  "data": {
    "commentId": "uuid-here",
    "text": "Great video!",
    "createdAt": "2026-10-02T00:00:00Z",
    "user": {
      "userId": "uuid-here",
      "username": "username"
    }
  }
}
```

### GET /videos/:videoId/comments
Retrieve comments for a video.

**Query Parameters:**
- `page`: Page number (default: 1)
- `limit`: Results per page (default: 20, max: 100)

**Response (200):**
```json
{
  "success": true,
  "data": {
    "comments": [
      {
        "commentId": "uuid-here",
        "text": "Great video!",
        "createdAt": "2026-10-02T00:00:00Z",
        "user": {
          "userId": "uuid-here",
          "username": "username"
        },
        "replies": []
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 150
    }
  }
}
```

---

## Channel Service Endpoints

### POST /channels/:channelId/subscribe
Subscribe to a channel.

**Headers:** `Authorization: Bearer <token>`

**Response (200):**
```json
{
  "success": true,
  "data": {
    "subscribed": true,
    "subscriberCount": 1200
  }
}
```

### GET /channels/:channelId
Get channel information.

**Response (200):**
```json
{
  "success": true,
  "data": {
    "channelId": "uuid-here",
    "name": "Channel Name",
    "description": "Channel description",
    "subscriberCount": 1200,
    "videoCount": 45,
    "createdAt": "2025-01-01T00:00:00Z"
  }
}
```

---

## Search Service Endpoints

### GET /search
Search for videos.

**Query Parameters:**
- `q`: Search query (required)
- `sort`: "relevance" | "date" | "views" (default: "relevance")
- `page`: Page number (default: 1)
- `limit`: Results per page (default: 20, max: 100)

**Response (200):**
```json
{
  "success": true,
  "data": {
    "results": [
      {
        "videoId": "uuid-here",
        "title": "Video Title",
        "thumbnailUrl": "https://cdn.namatube.com/thumbnails/...",
        "views": 1500,
        "uploadedAt": "2026-10-02T00:00:00Z",
        "channel": {
          "channelId": "uuid-here",
          "name": "Channel Name"
        }
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 345
    }
  }
}
```

---

## Recommendation Service Endpoints

### GET /recommendations
Get personalized video recommendations.

**Headers:** `Authorization: Bearer <token>` (optional)

**Query Parameters:**
- `limit`: Number of recommendations (default: 10, max: 50)

**Response (200):**
```json
{
  "success": true,
  "data": {
    "recommendations": [
      {
        "videoId": "uuid-here",
        "title": "Recommended Video",
        "thumbnailUrl": "https://cdn.namatube.com/thumbnails/...",
        "views": 2500,
        "channel": {
          "channelId": "uuid-here",
          "name": "Channel Name"
        }
      }
    ]
  }
}
```

---

## Rate Limiting
- **Authenticated users:** 1000 requests per hour
- **Unauthenticated users:** 100 requests per hour
- **Upload endpoints:** 10 uploads per hour per user

## Versioning
- Current version: `v1`
- Deprecated endpoints will be supported for 6 months after deprecation notice
- Breaking changes will result in a new version (`v2`, etc.)

## Change Log
- **2026-10-02:** Initial API contract v1.0.0
