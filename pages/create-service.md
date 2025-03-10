---
title: Create Service Page
project: meows
description: Interface for creating and editing service definitions
target: Frontend developers
detail_level: Page-level technical details
last_updated: 2024
tags: [pages, frontend, service, creation]
---

# Create Service Page (/personal/service/create)

## Overview

The Create Service page provides an interface for users to create new service definitions or edit existing ones. It offers a structured form with validation and preview capabilities to ensure services are properly configured.

## Route

```
/service/create  // For new services
/service/edit/[id]  // For editing existing services
```

## Page Components

### Service Form

- Service name input
- Command shortcut input
- URL template builder
- Parameter configuration
- Icon selection/upload
- Label assignment

### Template Builder

- URL pattern input with parameter highlighting
- Parameter definition fields
- Parameter validation rules
- Default value configuration

### Preview Section

- Live service preview
- Test execution capability
- Validation feedback
- Example usage

## User Flow

```mermaid
flowchart TD
    A[Create Service] --> B[Enter Basic Info]
    B --> C[Define URL Template]
    C --> D[Add Parameters]
    D --> E[Set Labels]
    E --> F[Preview]
    F --> G{Valid?}
    G -->|Yes| H[Save Service]
    G -->|No| I[Show Errors]
    I --> D
    H --> J[Success Message]
    J --> K[Return to Inventory]
```

## Functionality

### Service Validation

- Required fields: name, shortcut, URL template
- Shortcut uniqueness verification
- URL template syntax validation
- Parameter consistency check

### Parameter Configuration

- Name and description
- Type (string, number, boolean, enum)
- Required/optional status
- Default values
- Validation rules (regex, min/max length)

### Icon Management

- Automatic favicon fetching from domain
- Custom icon upload (PNG, SVG)
- Icon preview and cropping

## Related Components

- [ServiceBuilder Component](../components/ServiceBuilder.md)
- [ParameterEditor Component](../components/ParameterEditor.md)
- [IconSelector Component](../components/IconSelector.md)

## Related Pages

- [Inventory](inventory.md)
- [Global Catalog](global-catalog.md)
- [Service Details](service-details.md)
