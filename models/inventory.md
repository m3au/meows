---
title: Inventory Model
description: Inventory data model specification
detail_level: Data structure
tags: [model, inventory, data, commands, organization]
---

# Inventory Model

The Inventory model represents a user's personal collection of commands, organized with labels and metadata. Each user has a single inventory for their commands.

## Schema

```typescript
interface Inventory {
  id: string; // Unique identifier
  name: string; // Display name
  description?: string; // Optional description
  owner_id: string; // Reference to user who owns this inventory

  // Organization
  commands: Command[]; // Commands in this inventory
  labels: Label[]; // Labels used in this inventory

  // Metadata
  created_at: string; // Creation timestamp
  updated_at: string; // Last update timestamp
  last_used: string; // Last usage timestamp
  view_count: number; // Number of views (if public)
}
```

## Properties

| Property      | Type      | Description                                                 |
| ------------- | --------- | ----------------------------------------------------------- |
| `id`          | string    | Unique identifier for the inventory                         |
| `name`        | string    | Display name of the inventory                               |
| `description` | string    | Optional description of the inventory's purpose             |
| `owner_id`    | string    | Reference to the user who owns this inventory               |
| `commands`    | Command[] | Array of commands contained in this inventory               |
| `labels`      | Label[]   | Array of labels used to organize commands in this inventory |
| `created_at`  | string    | ISO timestamp of creation                                   |
| `updated_at`  | string    | ISO timestamp of last update                                |
| `last_used`   | string    | ISO timestamp of last usage                                 |
| `view_count`  | number    | Number of views if the inventory is public                  |

## Usage

The Inventory provides a way for users to organize their commands into a personal collection. This enables users to:

- Create different command sets for different contexts using labels
- Share specific commands with others
- Maintain organization structures for different purposes
- Customize their command collection to match their workflow

## Inventory Example

A user's inventory contains commands created or imported by the user:

```json
{
  "id": "inv_personal",
  "name": "My Commands",
  "description": "My everyday commands",
  "owner_id": "user123",
  "commands": [...],
  "labels": [...],
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-02-15T14:22:31Z",
  "last_used": "2024-03-01T09:15:42Z",
  "view_count": 0
}
```

## Inventory Operations

The system supports the following operations on the inventory:

- **Create**: Add new commands to the inventory
- **Read**: Retrieve inventory information and contents
- **Update**: Modify command properties and organization
- **Delete**: Remove commands from the inventory
- **Share**: Share specific commands with other users
- **Import**: Import commands from the global catalog
- **Export**: Export inventory for backup or sharing

## Storage and Synchronization

The inventory is stored in:

- **Client-side storage**: For offline access and performance
- **Server database**: For persistence and sharing

Synchronization uses a transaction-based approach with conflict resolution for concurrent edits from multiple devices.

## Related Models

- [User](user.md) - Owner of the inventory
- [Command](command.md) - Commands contained in the inventory
- [Label](label.md) - Labels used to organize commands in the inventory
- [Global Catalog](global-catalog.md) - System-wide catalog of shared commands

## Related Documentation

- [Command Management Flow](../flows/command-management.md)
- [Inventory Page](../pages/inventory.md)
- [Service Icon Component](../components/ServiceIcon.md)
