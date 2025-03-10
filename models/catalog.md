---
title: Catalog Model
project: meows
description: Catalog data model specification
target: Developers
detail_level: Data structure
last_updated: 2024
tags: [model, catalog, data, commands, organization]
---

# Catalog Model

The Catalog model represents a user's personal collection of commands, organized with labels and metadata. Each user can have multiple catalogs for different contexts or purposes.

## Schema

```typescript
interface Catalog {
  id: string; // Unique identifier
  name: string; // Display name
  description?: string; // Optional description
  owner_id: string; // Reference to user who owns this catalog

  // Organization
  commands: Command[]; // Commands in this catalog
  labels: Label[]; // Labels used in this catalog

  // Settings
  is_default: boolean; // Whether this is the user's default catalog
  is_public: boolean; // Whether this catalog is publicly visible

  // Metadata
  created_at: string; // Creation timestamp
  updated_at: string; // Last update timestamp
  last_used: string; // Last usage timestamp
  view_count: number; // Number of views (if public)
}
```

## Properties

| Property      | Type      | Description                                               |
| ------------- | --------- | --------------------------------------------------------- |
| `id`          | string    | Unique identifier for the catalog                         |
| `name`        | string    | Display name of the catalog                               |
| `description` | string    | Optional description of the catalog's purpose             |
| `owner_id`    | string    | Reference to the user who owns this catalog               |
| `commands`    | Command[] | Array of commands contained in this catalog               |
| `labels`      | Label[]   | Array of labels used to organize commands in this catalog |
| `is_default`  | boolean   | Whether this is the user's default catalog                |
| `is_public`   | boolean   | Whether this catalog is publicly visible to other users   |
| `created_at`  | string    | ISO timestamp of creation                                 |
| `updated_at`  | string    | ISO timestamp of last update                              |
| `last_used`   | string    | ISO timestamp of last usage                               |
| `view_count`  | number    | Number of views if the catalog is public                  |

## Usage

Catalogs provide a way for users to organize their commands into separate collections. This enables users to:

- Create different command sets for different contexts (work, personal, projects)
- Share specific collections with others
- Maintain separate organization structures for different purposes
- Switch between different command sets easily

## Catalog Types

### Personal Catalogs

Personal catalogs are private by default and contain commands created or imported by the user:

```json
{
  "id": "cat_personal",
  "name": "Personal",
  "description": "My everyday commands",
  "owner_id": "user123",
  "commands": [...],
  "labels": [...],
  "is_default": true,
  "is_public": false,
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-02-15T14:22:31Z",
  "last_used": "2024-03-01T09:15:42Z",
  "view_count": 0
}
```

### Shared Catalogs

Catalogs can be shared with specific users or made public:

```json
{
  "id": "cat_dev_tools",
  "name": "Development Tools",
  "description": "Common tools for web development",
  "owner_id": "user123",
  "commands": [...],
  "labels": [...],
  "is_default": false,
  "is_public": true,
  "created_at": "2024-01-15T00:00:00Z",
  "updated_at": "2024-02-20T11:42:31Z",
  "last_used": "2024-03-02T14:22:18Z",
  "view_count": 156
}
```

## Catalog Operations

The system supports the following operations on catalogs:

- **Create**: Add new catalogs
- **Read**: Retrieve catalog information and contents
- **Update**: Modify catalog properties and organization
- **Delete**: Remove catalogs (with confirmation for non-empty catalogs)
- **Share**: Make catalogs public or share with specific users
- **Import**: Import commands from other catalogs
- **Export**: Export catalogs for backup or sharing
- **Clone**: Create a copy of a catalog

## Storage and Synchronization

Catalogs are stored in:

- **Client-side storage**: For offline access and performance
- **Server database**: For persistence and sharing

Synchronization uses a transaction-based approach with conflict resolution for concurrent edits from multiple devices.

## Related Models

- [[user|User]] - Owner of the catalog
- [[command|Command]] - Commands contained in the catalog
- [[label|Label]] - Labels used to organize commands in the catalog
- [[global-catalog|Global Catalog]] - System-wide catalog of shared commands

## Related Documentation

- [[../flows/command-management|Command Management Flow]]
- [[../pages/personal-catalog|Personal Catalog Page]]
- [[../components/CatalogView|Catalog View Component]]
