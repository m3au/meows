---
title: SearchBar Component
project: meows
description: Documentation for the SearchBar component
target: Technical implementers
detail_level: Component details
last_updated: 2024
tags: [component, UI, search]
---

# SearchBar Component

The SearchBar is the primary command input mechanism in meows.space. It serves as the main entry point for user interaction, allowing users to enter commands and parameters.

## Structure

The SearchBar consists of three main sub-components:

1. **ProviderSelect** - A dropdown for choosing search engines
2. **CommandInput** - The main text field with parsing and suggestions
3. **ActionBar** - Contains execute/clear/settings buttons

## Functionality

### Command Input

The CommandInput field accepts text input from the user and performs real-time parsing to identify:

- Command keywords
- Parameters
- Special operators

### Auto-suggestions

As users type, the component provides suggestions based on:

- Command history
- Available commands
- Parameter hints

### Provider Selection

The ProviderSelect dropdown allows users to:

- Choose default search engines
- Override the default search provider for the current command
- Access recently used providers

### Action Controls

The ActionBar provides buttons for:

- Executing the current command
- Clearing the input field
- Accessing settings
- Viewing command history

## Technical Implementation

The SearchBar implements several key features:

- Real-time command parsing
- Command validation
- Parameter extraction
- History tracking
- Focus management

## Related Components

- [ServiceGrid Component](ServiceGrid.md)
- [LabelBar Component](LabelBar.md)
- [CommandBuilder Component](CommandBuilder.md)

## Usage in Pages

The SearchBar appears on multiple pages:

- Main Search (/)
- Inventory (/personal)
- Global Catalog (/catalog)
