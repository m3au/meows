---
title: Tag Model
project: meows
description: Tag data model specification
target: Developers
detail_level: Data structure
last_updated: 2024
tags: [model, tag, data]
---

# Tag Model

The Tag model implements the label-based organization system, allowing commands to be categorized and filtered. Tags can be applied to multiple commands and commands can have multiple tags.

## Schema

```typescript
interface Tag {
  id: string;
  name: string;
  color: string;
  services_count: number;
  created_at: string;
}
```

## Properties

| Property         | Type   | Description                                               |
| ---------------- | ------ | --------------------------------------------------------- |
| `id`             | string | Unique identifier for the tag                             |
| `name`           | string | Display name of the tag                                   |
| `color`          | string | Color code for visual representation (hex or named color) |
| `services_count` | number | Count of services using this tag                          |
| `created_at`     | string | ISO timestamp of creation                                 |

## Usage

Tags provide a flexible organization system for services, allowing users to categorize and filter their command collections. The system uses a flat label structure where each command can have multiple labels, enabling commands to appear in different contexts based on their categorization.

## Related Models

- [[service|Service]] - Services that can be tagged with this tag
- [[user-preferences|User Preferences]] - Stores user's tag ordering preferences

## Tag Types

### System Tags

System tags are predefined categories that come with the application:

```json
{
  "id": "search",
  "name": "Search",
  "color": "#4285F4",
  "services_count": 12,
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-01T00:00:00Z",
  "user_id": null
}
```

### User Tags

User tags are custom categories created by users:

```json
{
  "id": "work",
  "name": "Work",
  "color": "#34A853",
  "services_count": 5,
  "created_at": "2024-02-15T14:22:31Z",
  "updated_at": "2024-02-15T14:22:31Z",
  "user_id": "user123"
}
```

## Tag Usage

Tags are used throughout the application for:

1. **Filtering**: Narrowing down command lists
2. **Organization**: Grouping related commands
3. **Discovery**: Finding commands by category
4. **Visual Cues**: Color-coding in the UI

## Tag Operations

The system supports the following operations on tags:

- **Create**: Add new tags
- **Read**: Retrieve tag information
- **Update**: Modify tag properties
- **Delete**: Remove tags
- **Assign**: Associate tags with commands
- **Unassign**: Remove tag associations

## Storage and Synchronization

Tags are stored in:

- **IndexedDB**: Local persistent storage
- **Server Database**: For shared tags (optional)

Synchronization uses a CRDT-based approach with version tracking to resolve conflicts.

## UI Representation

Tags are visually represented as:

- **Tag Pills**: In the TagBar component
- **Tag Badges**: On command cards
- **Tag Filters**: In search interfaces
- **Tag Selectors**: In command editing forms

## Related Documentation

- [[../components/TagBar|TagBar Component]]
- [[../pages/personal-catalog|Personal Catalog Page]]
- [[../pages/global-catalog|Global Catalog Page]]
