---
title: Command Model
project: meows
description: Command data model specification and implementation details
target: Developers (frontend and backend)
detail_level: Technical implementation details
last_updated: 2024
tags: [models, data, command]
---

# Command Model

The Command model represents the core data structure for command definitions in meows.space. It defines the structure, properties, and behaviors of commands throughout the system.

## Data Structure

```typescript
interface Command {
  id: string; // Unique identifier
  name: string; // Display name
  prefix: string; // Command prefix (e.g., "g" for Google)
  url: string; // URL template with parameter placeholders
  icon: string; // Icon URL or data URI
  description: string; // User-friendly description
  labels: string[]; // Associated labels
  parameters: Parameter[]; // Parameter definitions
  metadata: Metadata; // Additional metadata
  created_at: string; // Creation timestamp
  updated_at: string; // Last update timestamp
  user_id?: string; // Owner (null for system commands)
}

interface Parameter {
  name: string; // Parameter name
  description: string; // Parameter description
  default_value?: string; // Optional default value
  required: boolean; // Whether parameter is required
  position: number; // Position in command string
}

interface Metadata {
  source: "system" | "user" | "community"; // Command origin
  visibility: "private" | "public"; // Visibility setting
  usage_count: number; // Usage statistics
  rating: number; // Community rating (1-5)
  version: number; // Version for sync
}
```

## Command Types

### Static Commands

Static commands have no parameters and map directly to a URL:

```json
{
  "id": "gmail",
  "name": "Gmail",
  "prefix": "gm",
  "url": "https://mail.google.com",
  "icon": "https://mail.google.com/favicon.ico",
  "description": "Open Gmail",
  "labels": ["email", "google"],
  "parameters": [],
  "metadata": {
    "source": "system",
    "visibility": "public",
    "usage_count": 0,
    "rating": 4.8,
    "version": 1
  }
}
```

### Dynamic Commands

Dynamic commands include parameters that are interpolated into the URL:

```json
{
  "id": "google-search",
  "name": "Google Search",
  "prefix": "g",
  "url": "https://google.com/search?q={query}",
  "icon": "https://google.com/favicon.ico",
  "description": "Search Google for {query}",
  "labels": ["search", "google"],
  "parameters": [
    {
      "name": "query",
      "description": "Search query",
      "required": true,
      "position": 0
    }
  ],
  "metadata": {
    "source": "system",
    "visibility": "public",
    "usage_count": 0,
    "rating": 4.9,
    "version": 1
  }
}
```

## Command Processing

1. **Parsing**: Extract prefix and parameters from input
2. **Resolution**: Match prefix to command definition
3. **Validation**: Ensure required parameters are provided
4. **Interpolation**: Replace parameter placeholders in URL template
5. **Execution**: Navigate to generated URL

## Storage and Synchronization

Commands are stored in:

- **IndexedDB**: Local persistent storage
- **Server Database**: For shared commands (optional)

Synchronization uses a CRDT-based approach with version tracking to resolve conflicts.

## Related Models

- [Label Model](label.md) - For command categorization
- [User Profile Model](user-profile.md) - For command ownership
- [User Preferences Model](user-preferences.md) - For command defaults

## Related Documentation

- [Command Execution Flow](../flows/command-execution.md)
- [Command Management Flow](../flows/command-management.md)
- [Inventory Page](../pages/inventory.md)
- [Global Catalog Page](../pages/global-catalog.md)
