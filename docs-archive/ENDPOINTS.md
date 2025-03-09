---
name: ENDPOINTS
project: meows
description: API endpoints documentation, data models, and integration guidelines
target: Backend developers and API integrators
detail_level: API specification and implementation details
last_updated: 2024
directives: |
  1. Document only what exists
  2. No marketing language
  3. No buzzwords
  4. No feature promises
  5. No code generation
  6. No user-friendly explanations
  7. No redundant text
  8. No colors in diagrams
  9. No business stakeholder language
  10. No hypotheticals
  11. Don't touch the table of contents
---

# API Endpoints <!-- omit from toc -->

## Table of Contents <!-- omit from toc -->

- [Authentication Endpoints](#authentication-endpoints)
  - [`/api/auth`](#apiauth)
- [Service Management](#service-management)
  - [`/api/services`](#apiservices)
  - [`/api/tags`](#apitags)
- [User Data](#user-data)
  - [`/api/user`](#apiuser)
- [Search Providers](#search-providers)
  - [`/api/providers`](#apiproviders)
- [Analytics](#analytics)
  - [`/api/analytics`](#apianalytics)
- [Data Models](#data-models)
  - [Service Object](#service-object)
  - [Tag Object](#tag-object)
  - [User Preferences](#user-preferences)
- [Error Handling](#error-handling)
  - [Error Response Format](#error-response-format)
  - [Common Error Codes](#common-error-codes)
- [Rate Limiting](#rate-limiting)
- [Caching](#caching)
  - [Cache Headers](#cache-headers)
  - [Cached Endpoints](#cached-endpoints)

## Authentication Endpoints

### `/api/auth`

- POST `/login` - User login
- POST `/logout` - User logout
- POST `/register` - New user registration
- GET `/session` - Get current session
- POST `/refresh` - Refresh access token

## Service Management

### `/api/services`

- GET `/` - List all services
- GET `/:id` - Get service details
- POST `/` - Create new service
- PUT `/:id` - Update service
- DELETE `/:id` - Delete service
- GET `/search` - Search services
  - Query params:
    - `q`: Search query
    - `tags`: Filter by tags
    - `mode`: Search mode
    - `sort`: Sort method

### `/api/tags`

- GET `/` - List all tags
- POST `/` - Create new tag
- PUT `/:id` - Update tag
- DELETE `/:id` - Delete tag
- GET `/trending` - Get trending tags

## User Data

### `/api/user`

- GET `/preferences` - Get user preferences
- PUT `/preferences` - Update preferences
- GET `/history` - Get search history
- DELETE `/history` - Clear history
- GET `/favorites` - Get favorite services
- POST `/favorites/:id` - Add to favorites
- DELETE `/favorites/:id` - Remove from favorites

## Search Providers

### `/api/providers`

- GET `/` - List search providers
- GET `/:id/search` - Execute provider search
- GET `/default` - Get default provider
- PUT `/default` - Set default provider

## Analytics

### `/api/analytics`

- POST `/event` - Log user event
- GET `/trending` - Get trending services
- GET `/popular` - Get popular services
- GET `/metrics` - Get usage metrics

## Data Models

### Service Object

```typescript
interface Service {
  id: string;
  name: string;
  icon: string;
  url: string;
  tags: string[];
  metadata: {
    description: string;
    provider: string;
    metrics: {
      uses: number;
      rating: number;
    };
  };
  created_at: string;
  updated_at: string;
}
```

### Tag Object

```typescript
interface Tag {
  id: string;
  name: string;
  color: string;
  services_count: number;
  created_at: string;
}
```

### User Preferences

```typescript
interface UserPreferences {
  default_provider: string;
  grid_layout: {
    columns: number;
    spacing: number;
  };
  tags_order: string[];
  theme: "light" | "dark" | "system";
  behavior: {
    click_action: "single" | "double";
    new_tab: boolean;
  };
}
```

## Error Handling

### Error Response Format

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

### Common Error Codes

- `AUTH_REQUIRED` - Authentication required
- `INVALID_INPUT` - Invalid request parameters
- `NOT_FOUND` - Resource not found
- `RATE_LIMITED` - Too many requests
- `SERVER_ERROR` - Internal server error

## Rate Limiting

- 100 requests per minute per user
- 1000 requests per hour per IP
- Unlimited for authenticated users with premium status

## Caching

### Cache Headers

```http
Cache-Control: public, max-age=300
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
```

### Cached Endpoints

- GET `/api/services` - 5 minutes
- GET `/api/tags` - 5 minutes
- GET `/api/providers` - 1 hour
- GET `/api/analytics/trending` - 1 hour
