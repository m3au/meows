---
title: User Preferences Model
description: User Preferences data model specification
detail_level: Data structure
tags: [model, user-preferences, data]
revised: false
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
  grid_order: {
    [labelId: string]: string[]; // Map of label ID to array of service IDs in order
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

| Property                | Type                    | Description                                        |
| ----------------------- | ----------------------- | -------------------------------------------------- |
| `default_provider`      | string                  | ID of the default search provider                  |
| `grid_layout.columns`   | number                  | Number of columns in the service grid              |
| `grid_layout.spacing`   | number                  | Spacing between grid items (in pixels)             |
| `grid_order`            | Object<string,string[]> | Custom ordering of services by label ID            |
| `labels_order`          | string[]                | Ordered array of label IDs for display             |
| `theme`                 | string                  | UI theme preference ("light", "dark", or "system") |
| `behavior.click_action` | string                  | Action trigger type ("single" or "double" click)   |
| `behavior.new_tab`      | boolean                 | Whether to open services in a new tab              |

## Grid Ordering

The `grid_order` property stores user-defined custom ordering of services in the grid:

- Each key in the object is a label ID (or "all" for the unfiltered view)
- Each value is an array of service IDs in the user's preferred order
- When a user drags and drops services to reorder them, this property is updated
- If no custom order exists for a label, default sorting is applied (alphabetical, etc.)
- Example:

```json
"grid_order": {
  "all": ["svc_google", "svc_github", "svc_gmail", "svc_youtube"],
  "work": ["svc_github", "svc_jira", "svc_slack"],
  "personal": ["svc_gmail", "svc_youtube", "svc_twitter"]
}
```

## Usage

User preferences control the appearance and behavior of the application for each user. These settings are synchronized across devices and persist between sessions.

## Related Models

- [User Profile](user-profile.md) - The user profile that owns these preferences
- [Label](label.md) - Labels referenced in the labels_order property
- [Service](service.md) - Services referenced in the grid_order property

## Related Documentation

- [Settings Page](../pages/settings.md)
- [ServiceGrid Component](../components/ServiceGrid.md)
- Technical Implementation (Documentation moved)
