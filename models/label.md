---
title: Label Model
project: meows
description: Label data model specification
target: Developers
detail_level: Data structure
last_updated: 2024
tags: [model, label, data]
---

# Label Model

The Label model implements the label-based organization system, allowing commands to be categorized and filtered. Labels can be applied to multiple commands and commands can have multiple labels.

## Schema

```typescript
interface Label {
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
| `id`             | string | Unique identifier for the label                           |
| `name`           | string | Display name of the label                                 |
| `color`          | string | Color code for visual representation (hex or named color) |
| `services_count` | number | Count of services using this label                        |
| `created_at`     | string | ISO timestamp of creation                                 |

## Usage

Labels provide a flexible organization system for services, allowing users to categorize and filter their command collections. The system uses a flat label structure where each command can have multiple labels, enabling commands to appear in different contexts based on their categorization.

## Related Models

- [[service|Service]] - Services that can be labeled with this label
- [[user-preferences|User Preferences]] - Stores user's label ordering preferences

## Label Types

### System Labels

System labels are predefined categories that come with the application:

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

### User Labels

User labels are custom categories created by users:

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

## Label Usage

Labels are used throughout the application for:

1. **Filtering**: Narrowing down command lists
2. **Organization**: Grouping related commands
3. **Discovery**: Finding commands by category
4. **Visual Cues**: Color-coding in the UI

## Label Operations

The system supports the following operations on labels:

- **Create**: Add new labels
- **Read**: Retrieve label information
- **Update**: Modify label properties
- **Delete**: Remove labels
- **Assign**: Associate labels with commands
- **Unassign**: Remove label associations

## Storage and Synchronization

Labels are stored in:

- **IndexedDB**: Local persistent storage
- **Server Database**: For shared labels (optional)

Synchronization uses a CRDT-based approach with version tracking to resolve conflicts.

## UI Representation

Labels are visually represented as:

- **Label Pills**: In the LabelBar component
- **Label Badges**: On command cards
- **Label Filters**: In search interfaces
- **Label Selectors**: In command editing forms

## Related Documentation

- [[../components/LabelBar|LabelBar Component]]
- [[../pages/personal-catalog|Personal Catalog Page]]
- [[../pages/global-catalog|Global Catalog Page]]
