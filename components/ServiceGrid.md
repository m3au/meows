---
title: ServiceGrid Component
description: Documentation for the ServiceGrid component
detail_level: Component details
tags: [component, UI, grid]
revised: false
---

# ServiceGrid Component

The ServiceGrid displays commands as Windows 95-style icons in a grid layout. It serves as the primary visual interface for browsing and accessing commands.

## Structure

The ServiceGrid implements a responsive grid layout with the following features:

- Virtual grid rendering for performance optimization
- Icon display with labels underneath
- Visual indicators for command type and status
- Context menus for command actions
- Customizable grid ordering through drag-and-drop

## Functionality

### Virtual Rendering

The grid uses windowed rendering that creates DOM elements only for items in the viewport, providing:

- Stable performance with large command sets
- Reduced memory usage
- Smooth scrolling experience

### Icon Display

Each command is represented by an icon with:

- Automatically fetched domain favicon or custom icon
- Command name displayed underneath
- Visual indicators for command type (static/dynamic)
- Status indicators (public/private, new, updated)

### Context Menus

Right-clicking on icons provides context menus with actions:

- Edit command
- Delete command
- Duplicate command
- Add to favorites
- Share command
- View usage statistics

### Interaction

The grid supports several interaction patterns:

- Click to execute command
- Drag-and-drop for organization and custom ordering
- Multi-select for batch operations
- Hover for command details

### Custom Ordering

The ServiceGrid implements a persistent custom ordering system:

- Users can drag and drop icons to create a custom arrangement
- The custom order is saved to user preferences automatically
- Order is preserved across sessions and devices
- Different orders can be maintained for different labels/views
- Default sorting options (alphabetical, recent, etc.) are available when no custom order exists

## Technical Implementation

The ServiceGrid implements several key features:

- Virtualized grid rendering
- Responsive layout adaptation
- Lazy image loading
- Drag-and-drop functionality with order persistence
- Context menu system
- Order synchronization with user preferences

## Related Components

- [SearchBar Component](SearchBar.md)
- [LabelBar Component](LabelBar.md)
- [ServiceBuilder Component](ServiceBuilder.md)

## Usage in Pages

The ServiceGrid appears on multiple pages:

- Main Search (/)
- Inventory (/personal)
- Global Catalog (/catalog)

## Related Models

- [User Preferences Model](../models/user-preferences.md) - Stores the user's custom grid ordering
- [Inventory Model](../models/inventory.md) - Contains the commands displayed in the grid
