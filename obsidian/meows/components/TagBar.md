---
title: TagBar Component
project: meows
description: Documentation for the TagBar component
target: Technical implementers
detail_level: Component details
last_updated: 2024
tags: [component, UI, tags, labels]
---

# TagBar Component

The TagBar provides category-based filtering for commands. It allows users to filter the command grid by selecting one or more labels.

## Structure

The TagBar implements a horizontal scrolling interface with the following features:

- Horizontal scrolling tag list
- Tag pills showing category names and command counts
- Multiple selection for combined filtering
- Visual indicators for active tags

## Functionality

### Label Display

The TagBar displays labels as interactive pills that show:
- Label name
- Command count for each label
- Visual indicator for active state

### Filtering

The component enables filtering through:
- Single label selection
- Multiple label selection (AND operation)
- Label toggling
- Clear all filters option

### Navigation

The TagBar provides navigation features:
- Horizontal scrolling for many labels
- Overflow indicators
- Scroll buttons for desktop
- Touch/swipe support for mobile

### Organization

Labels can be:
- Reordered through drag-and-drop
- Pinned to always appear first
- Hidden from the main view
- Grouped into categories

## Technical Implementation

The TagBar implements several key features:

- Horizontal virtualized list
- Drag-and-drop reordering
- Responsive design for different screen sizes
- Touch and mouse interaction support
- Visual feedback for selection states

## Related Components

- [[SearchBar|SearchBar Component]]
- [[ServiceGrid|ServiceGrid Component]]
- [[CommandBuilder|CommandBuilder Component]]

## Usage in Pages

The TagBar appears on multiple pages:
- Personal Catalog (/personal)
- Global Catalog (/catalog) 
