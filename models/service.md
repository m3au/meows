---
title: Service Model
project: meows
description: Service data model specification and implementation details
target: Developers (frontend and backend)
detail_level: Technical implementation details
last_updated: 2024
tags: [models, data, service]
---

# Service Model

The Service model represents the core entity for services in meows.space. A service is a command template that can be executed to generate a URL.

## Data Structure

```typescript
interface Service {
  id: string;                 // Unique identifier
  name: string;               // Display name
  icon: string;               // Icon URL or data URI
  url: string;                // URL template with parameter placeholders
  tags: string[];             // Associated tags/labels
  metadata: {
    description: string;      // User-friendly description
    provider: string;         // Service provider
    metrics: {
      uses: number;           // Usage count
      rating: number;         // Community rating (1-5)
    };
  };
  created_at: string;         // Creation timestamp
  updated_at: string;         // Last update timestamp
}
```

## Service Types

### System Services

Pre-defined services that come with the application:

```json
{
  "id": "google-search",
  "name": "Google Search",
  "icon": "https://google.com/favicon.ico",
  "url": "https://google.com/search?q={query}",
  "tags": ["search", "google"],
  "metadata": {
    "description": "Search Google for {query}",
    "provider": "Google",
    "metrics": {
      "uses": 1245678,
      "rating": 4.9
    }
  },
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-01T00:00:00Z"
}
```

### User Services

Custom services created by users:

```json
{
  "id": "jira-ticket",
  "name": "JIRA Ticket",
  "icon": "https://jira.atlassian.com/favicon.ico",
  "url": "https://company.atlassian.net/browse/{ticket}",
  "tags": ["work", "development"],
  "metadata": {
    "description": "Open JIRA ticket {ticket}",
    "provider": "Atlassian",
    "metrics": {
      "uses": 42,
      "rating": 0
    }
  },
  "created_at": "2024-02-15T14:22:31Z",
  "updated_at": "2024-02-15T14:22:31Z"
}
```

## Service Operations

The system supports the following operations on services:

- **Create**: Add new services
- **Read**: Retrieve service information
- **Update**: Modify service properties
- **Delete**: Remove services
- **Execute**: Generate URL and navigate
- **Share**: Publish to community catalog

## Storage and Synchronization

Services are stored in:

- **IndexedDB**: Local persistent storage
- **Server Database**: For shared services (optional)

Synchronization uses a CRDT-based approach with version tracking to resolve conflicts.

## UI Representation

Services are visually represented as:

- **Service Cards**: In the ServiceGrid component
- **Command Items**: In command history
- **Search Results**: In search interfaces

## Related Models

- [[command|Command Model]] - Legacy model (Service is the newer implementation)
- [[tag|Tag Model]] - For service categorization
- [[user-profile|User Profile Model]] - For service ownership

## Related Documentation

- [[../components/ServiceGrid|ServiceGrid Component]]
- [[../pages/personal-catalog|Personal Catalog Page]]
- [[../pages/global-catalog|Global Catalog Page]] 
