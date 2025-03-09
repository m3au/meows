---
title: CommandBuilder Component
project: meows
description: Documentation for the CommandBuilder component
target: Technical implementers
detail_level: Component details
last_updated: 2024
tags: [component, UI, command, creation]
---

# CommandBuilder Component

The CommandBuilder enables command creation and editing. It provides a comprehensive interface for defining and configuring commands.

## Structure

The CommandBuilder implements a multi-step form interface with the following features:

- Command name input
- URL template builder
- Parameter configuration
- Label assignment
- Test functionality
- Privacy controls

## Functionality

### Command Definition

The component allows users to define commands with:

- Command name and description
- Command key (invocation shortcut)
- URL template
- Command type (static/dynamic)

### Parameter Configuration

For dynamic commands, users can configure parameters:

- Parameter names
- Placeholder text
- Required/optional status
- Default values
- Validation rules

### URL Template Builder

The URL template builder provides:

- Visual template construction
- Parameter insertion points
- Template validation
- URL preview with sample parameters

### Label Management

The label management section allows:

- Assigning existing labels
- Creating new labels
- Removing labels from command
- Setting primary label

### Testing

The test functionality enables:

- Entering test parameters
- Previewing constructed URL
- Test execution in new tab
- Validation feedback

### Privacy Settings

Privacy controls allow setting:

- Private (only visible to owner)
- Public (visible in global catalog)
- Sharing permissions

## Technical Implementation

The CommandBuilder implements several key features:

- Multi-step form validation
- Real-time URL template preview
- Parameter validation
- Command uniqueness checking
- Template syntax highlighting

## Related Components

- [[SearchBar|SearchBar Component]]
- [[ServiceGrid|ServiceGrid Component]]
- [[TagBar|TagBar Component]]

## Usage in Pages

The CommandBuilder appears on:

- Personal Catalog (/personal) - for creating/editing commands
- Service Details (/service/[id]) - for viewing/editing command details
