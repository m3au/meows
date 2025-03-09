---
name: COMPONENTS
project: meows
description: Detailed breakdown of UI components, their relationships, and organization
target: Frontend developers and UI/UX designers
detail_level: Component-level technical details
last_updated: 2024
directives: |
  1. Document only what exists
  2. No marketing language
  3. No buzzwords
  4. No feature promises
  5. No code generation
  6. No user-friendly explanations
  7. No redundant text
  8. No colors in diagrams
  9. No business stakeholder language
  10. No hypotheticals
  11. Don't touch the table of contents
---

# Component Architecture <!-- omit from toc -->

## Table of Contents <!-- omit from toc -->

- [Page Components](#page-components)
  - [MainSearch.tsx (/)](#mainsearchtsx-)
  - [PersonalCatalog.tsx (/personal)](#personalcatalogtsx-personal)
  - [GlobalCatalog.tsx (/catalog)](#globalcatalogtsx-catalog)
- [Shared Components](#shared-components)
  - [Data Display](#data-display)
  - [Inputs](#inputs)
  - [UI Elements](#ui-elements)
- [Component State](#component-state)
  - [Local State](#local-state)
  - [Global State](#global-state)

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
