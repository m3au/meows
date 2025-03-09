---
title: Error Response Model
project: meows
description: Error Response data model specification
target: Developers
detail_level: Data structure
last_updated: 2024
tags: [model, error, data]
---

# Error Response Model

The Error Response model defines the standardized format for API error responses across the system.

## Schema

```typescript
interface ErrorResponse {
  error: {
    code: string;
    message: string;
    details?: any;
  };
  status: number;
}
```

## Properties

| Property        | Type   | Description                       |
| --------------- | ------ | --------------------------------- |
| `error.code`    | string | Machine-readable error code       |
| `error.message` | string | Human-readable error message      |
| `error.details` | any    | Optional additional error details |
| `status`        | number | HTTP status code                  |

## Common Error Codes

- `AUTH_REQUIRED` - Authentication required
- `INVALID_INPUT` - Invalid request parameters
- `NOT_FOUND` - Resource not found
- `RATE_LIMITED` - Too many requests
- `SERVER_ERROR` - Internal server error

## Usage

Error responses are returned by API endpoints when an error occurs. The standardized format ensures consistent error handling across the application.

## Related Documentation

- [[technical/system-integration|System Integration]] - For API integration guidelines
