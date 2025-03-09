---
title: User Preferences Model
project: meows
description: User preferences data model specification and implementation details
target: Developers (frontend and backend)
detail_level: Technical implementation details
last_updated: 2024
tags: [models, data, user, preferences]
---

# User Preferences Model

The User Preferences model represents the customizable settings that control the behavior and appearance of the application for each user.

## Data Structure

```typescript
interface UserPreferences {
  default_provider: string;       // Default search provider
  grid_layout: {
    columns: number;              // Number of grid columns
    spacing: number;              // Grid spacing in pixels
  };
  tags_order: string[];           // Ordered list of tag IDs
  theme: "light" | "dark" | "system"; // Theme preference
  behavior: {
    click_action: "single" | "double"; // Click behavior
    new_tab: boolean;             // Open in new tab
    history_limit: number;        // Command history limit
    suggestions: boolean;         // Show suggestions
  };
  display: {
    show_descriptions: boolean;   // Show command descriptions
    icon_size: "small" | "medium" | "large"; // Icon size
    font_size: number;            // Font size in pixels
  };
  sync: {
    enabled: boolean;             // Sync enabled
    frequency: "realtime" | "hourly" | "daily"; // Sync frequency
    include_history: boolean;     // Include history in sync
  };
}
```

## Default Values

The system provides sensible defaults for all preferences:

```json
{
  "default_provider": "google",
  "grid_layout": {
    "columns": 4,
    "spacing": 16
  },
  "tags_order": [],
  "theme": "system",
  "behavior": {
    "click_action": "single",
    "new_tab": true,
    "history_limit": 100,
    "suggestions": true
  },
  "display": {
    "show_descriptions": true,
    "icon_size": "medium",
    "font_size": 14
  },
  "sync": {
    "enabled": true,
    "frequency": "realtime",
    "include_history": true
  }
}
```

## Preference Categories

### Interface Preferences

Control the visual appearance of the application:
- Theme selection
- Grid layout
- Icon size
- Font settings

### Behavior Preferences

Control how the application responds to user actions:
- Click behavior
- Tab opening
- History management
- Suggestions

### Provider Preferences

Control search and command providers:
- Default search engine
- Provider order
- Provider-specific settings

### Synchronization Preferences

Control data synchronization:
- Sync enabled/disabled
- Sync frequency
- Data inclusion

## Storage and Synchronization

User preferences are stored in:

- **IndexedDB**: Local persistent storage
- **Server Database**: For cross-device sync (optional)

Preferences are synchronized across devices when the user is logged in.

## Application

User preferences are applied:

1. **On Load**: When the application starts
2. **On Change**: Immediately when preferences are updated
3. **On Sync**: When changes are received from other devices

## Related Models

- [[user-profile|User Profile Model]] - For preference ownership
- [[command|Command Model]] - For command-specific preferences
- [[tag|Tag Model]] - For tag display preferences

## Related Documentation

- [[../pages/settings|Settings Page]]
- [[../technical/technology|Technical Implementation]] 
