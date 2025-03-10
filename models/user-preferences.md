---
title: User Preferences Model
description: User Preferences data model specification
detail_level: Data structure
tags: [model, user-preferences, data]
---

# User Preferences Model

The User Preferences model stores user-specific settings including theme preferences, default behaviors, and interface configurations.

## Schema

```typescript
interface UserPreferences {
  default_provider: string;
  grid_layout: {
    columns: number;
    spacing: number;
  };
  labels_order: string[];
  theme: "light" | "dark" | "system";
  behavior: {
    click_action: "single" | "double";
    new_tab: boolean;
  };
}
```

## Properties

| Property                | Type     | Description                                        |
| ----------------------- | -------- | -------------------------------------------------- |
| `default_provider`      | string   | ID of the default search provider                  |
| `grid_layout.columns`   | number   | Number of columns in the service grid              |
| `grid_layout.spacing`   | number   | Spacing between grid items (in pixels)             |
| `labels_order`          | string[] | Ordered array of label IDs for display             |
| `theme`                 | string   | UI theme preference ("light", "dark", or "system") |
| `behavior.click_action` | string   | Action trigger type ("single" or "double" click)   |
| `behavior.new_tab`      | boolean  | Whether to open services in a new tab              |

## Usage

User preferences control the appearance and behavior of the application for each user. These settings are synchronized across devices and persist between sessions.

## Related Models

- [User Profile](user-profile.md) - The user profile that owns these preferences
- [Label](label.md) - Labels referenced in the labels_order property

## Related Documentation

- [Settings Page](../pages/settings.md)
- Technical Implementation (Documentation moved)
