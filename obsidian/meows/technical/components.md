---
title: Component Architecture
project: meows
description: Detailed breakdown of UI components, their relationships, and organization
target: Frontend developers and UI/UX designers
detail_level: Component-level technical details
last_updated: 2024
tags: [components, frontend, UI, architecture]
---

# Component Architecture

## Page Components

### MainSearch.tsx (/)

```mermaid
graph TD
    A[MainSearch] --> B[SearchBar]
    A --> C[RecentCommands]

    B --> D[ProviderSelect]
    B --> E[CommandInput]
    B --> F[ActionBar]

    C --> G[CommandList]
    G --> H[CommandItem]
```

Components:

- `SearchBar` - Main command input container
  - `ProviderSelect` - Search engine dropdown
  - `CommandInput` - Command parsing & suggestions
  - `ActionBar` - Execute/clear/settings
- `RecentCommands` - Command history
  - `CommandList` - Virtual list of recent commands
  - `CommandItem` - Individual command with metadata

### PersonalCatalog.tsx (/personal)

```mermaid
graph TD
    A[PersonalCatalog] --> B[SearchHeader]
    A --> C[ServiceGrid]
    A --> D[TagBar]

    B --> E[SearchInput]
    B --> F[FilterControls]

    C --> G[ServiceCard]
    G --> H[ContextMenu]

    D --> I[TagList]
    I --> J[TagPill]
```

Components:

- `SearchHeader` - Search and filtering
  - `SearchInput` - Full-text search
  - `FilterControls` - Tag/sort controls
- `ServiceGrid` - Virtual grid of services
  - `ServiceCard` - Service with metadata
  - `ContextMenu` - Service actions
- `TagBar` - Tag navigation
  - `TagList` - Horizontal virtual list
  - `TagPill` - Individual tag with count

### GlobalCatalog.tsx (/catalog)

```mermaid
graph TD
    A[GlobalCatalog] --> B[CatalogHeader]
    A --> C[ServiceGrid]
    A --> D[TagBar]

    B --> E[SearchInput]
    B --> F[SortControls]

    C --> G[ServiceCard]
    G --> H[AddButton]
    G --> I[MetricsBar]
```

Components:

- `CatalogHeader` - Global search
  - `SearchInput` - Service search
  - `SortControls` - Popularity/recent
- `ServiceGrid` - Infinite loading grid
  - `ServiceCard` - Service preview
    - `AddButton` - Add to personal
    - `MetricsBar` - Usage stats
- `TagBar` - Category navigation

## Shared Components

### Data Display

- `VirtualGrid` - Windowed grid renderer
- `VirtualList` - Windowed list renderer
- `InfiniteLoader` - Load more trigger

### Inputs

- `CommandParser` - Command tokenization
- `Typeahead` - Real-time suggestions
- `SearchInput` - Full-text search

### UI Elements

- `IconButton` - Action buttons
- `DropdownMenu` - Context menus
- `Toast` - Status notifications

## Component State

### Local State

- Form inputs
- UI interactions
- Animation states

### Global State

- Search queries
- Selected services
- Active tags
- Command history

## Related Documentation

- [[../components/index|UI Components Overview]]
- [[../components/SearchBar|SearchBar Component]]
- [[../components/ServiceGrid|ServiceGrid Component]]
- [[../components/TagBar|TagBar Component]]
- [[../components/CommandBuilder|CommandBuilder Component]]
- [[pages|Page Structure]] 
