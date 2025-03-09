---
title: Tag Model
project: meows
description: Tag data model specification and implementation details
target: Developers (frontend and backend)
detail_level: Technical implementation details
last_updated: 2024
tags: [models, data, tag]
---

# Tag Model

The Tag model represents the categorization system for commands in meows.space. Tags provide a flexible way to organize and filter commands across the application.

## Data Structure

```typescript
interface Tag {
  id: string;                 // Unique identifier
  name: string;               // Display name
  color: string;              // Color code (hex)
  services_count: number;     // Number of associated commands
  created_at: string;         // Creation timestamp
  updated_at: string;         // Last update timestamp
  user_id?: string;           // Owner (null for system tags)
}
```

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

## Related Models

- [[command|Command Model]] - For tag associations
- [[user-profile|User Profile Model]] - For tag ownership
- [[user-preferences|User Preferences Model]] - For tag display preferences

## Related Documentation

- [[../components/TagBar|TagBar Component]]
- [[../pages/personal-catalog|Personal Catalog Page]]
- [[../pages/global-catalog|Global Catalog Page]] 
