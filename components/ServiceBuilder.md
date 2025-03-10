---
title: ServiceBuilder Component
project: meows
description: Documentation for the ServiceBuilder component
target: Technical implementers
detail_level: Component details
last_updated: 2024
tags: [component, UI, service, creation]
---

# ServiceBuilder Component

The ServiceBuilder enables service creation and editing. It provides a comprehensive interface for defining and configuring service URL templates.

## Structure

The ServiceBuilder implements a multi-step form interface with the following features:

- Service name input
- URL template builder
- Parameter configuration
- Label assignment
- Test functionality
- Privacy controls

## Functionality

### Service Definition

The component allows users to define services with:

- Service name and description
- Command key (invocation shortcut)
- URL template
- Service type (static/dynamic)

### Parameter Configuration

For dynamic services, users can configure parameters:

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
- Removing labels from service
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

The ServiceBuilder implements several key features:

- Multi-step form validation
- Real-time URL template preview
- Parameter validation
- Service uniqueness checking
- Template syntax highlighting

## Related Components

- [SearchBar Component](SearchBar.md)
- [ServiceGrid Component](ServiceGrid.md)
- [LabelBar Component](LabelBar.md)

## Usage in Pages

The ServiceBuilder appears on multiple pages:

- Inventory (/personal) - for creating/editing services
- Service Details (/catalog/service/:id) - for customizing before import
