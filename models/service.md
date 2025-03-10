---
title: Service Model
project: meows
description: Service data model specification
target: Developers
detail_level: Data structure
last_updated: 2024
tags: [model, service, data]
---

# Service Model

The Service model represents metadata for a command or service in the system, including visual representation, usage statistics, and categorization.

## Schema

```typescript
interface Service {
  id: string;
  name: string;
  icon: string;
  url: string;
  labels: string[];
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

## Properties

| Property                  | Type     | Description                                     |
| ------------------------- | -------- | ----------------------------------------------- |
| `id`                      | string   | Unique identifier for the service               |
| `name`                    | string   | Display name of the service                     |
| `icon`                    | string   | URL or data URI for the service icon            |
| `url`                     | string   | URL template for the service                    |
| `labels`                  | string[] | Array of label IDs associated with this service |
| `metadata.description`    | string   | Detailed description of the service             |
| `metadata.provider`       | string   | Provider or creator of the service              |
| `metadata.metrics.uses`   | number   | Count of service usage                          |
| `metadata.metrics.rating` | number   | Average user rating (1-5)                       |
| `created_at`              | string   | ISO timestamp of creation                       |
| `updated_at`              | string   | ISO timestamp of last update                    |

## Usage

Services are used to represent commands in the UI, providing visual and descriptive information for the user. They connect to the underlying Command model which handles the actual URL template and parameter extraction.

## Related Models

- [Command](command.md) - Defines the URL template and parameter extraction logic
- [Label](label.md) - Provides categorization for services

## Service Types

### System Services

Pre-defined services that come with the application:

```json
{
  "id": "google-search",
  "name": "Google Search",
  "icon": "https://google.com/favicon.ico",
  "url": "https://google.com/search?q={query}",
  "labels": ["search", "google"],
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
  "labels": ["work", "development"],
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

## Related Documentation

- [Command Execution Flow](../flows/command-execution.md)
- [Service Details Page](../pages/service-details.md)
- [Inventory Page](../pages/inventory.md)
- [Global Catalog Page](../pages/global-catalog.md)
