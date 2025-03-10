---
title: ServiceIcon Component
description: Visual representation of a service with favicon and label
detail_level: Component
tags: [component, UI, service, icon, favicon]
---

# ServiceIcon Component

The ServiceIcon component provides a visual representation of a command in the ServiceGrid. It displays the command's favicon and name in a Windows 95-style icon format.

## Visual Structure

```mermaid
graph TD
    subgraph "ServiceIcon Component"
        direction TB
        Icon[Favicon]
        Label[Service Name]
    end

    Icon --> Label
```

The ServiceIcon displays a favicon image at the top and the service name as a label below it. The component uses a standardized size and styling to create a uniform grid appearance, similar to desktop icons in traditional operating systems.

## Component API

```typescript
interface ServiceIconProps {
  service: {
    id: string;
    name: string;
    icon?: string;
    url: string;
  };
  isSelected?: boolean;
  onClick?: (serviceId: string) => void;
  onDoubleClick?: (serviceId: string) => void;
  onContextMenu?: (event: React.MouseEvent, serviceId: string) => void;
}
```

## Behavior

The ServiceIcon implements the following behaviors:

- **Icon Display**: Shows the service's favicon, either from the domain or a custom icon
- **Fallback Icon**: Displays a default icon when no favicon is available
- **Label Display**: Shows the service name below the icon
- **Selection State**: Visually indicates when the service is selected
- **Click Handling**: Processes single clicks for selection
- **Double-Click Handling**: Processes double clicks for execution
- **Context Menu**: Supports right-click for additional options
- **Drag and Drop**: Enables drag-and-drop for organization

## States

The ServiceIcon can exist in several states:

- **Default**: Normal display state
- **Selected**: Visually highlighted when selected
- **Hover**: Visual feedback when the mouse is over the icon
- **Dragging**: Visual state during drag operations
- **Loading**: Shown while the favicon is loading
- **Error**: Displayed when the favicon fails to load

## Usage Example

```jsx
<ServiceIcon
  service={{
    id: "svc_google",
    name: "Google",
    icon: "https://www.google.com/favicon.ico",
    url: "https://www.google.com",
  }}
  isSelected={false}
  onClick={(id) => console.log(`Selected service: ${id}`)}
  onDoubleClick={(id) => console.log(`Executing service: ${id}`)}
  onContextMenu={(event, id) => console.log(`Context menu for: ${id}`)}
/>
```

## Favicon Handling

The ServiceIcon implements several strategies for favicon handling:

- **Direct URL**: Uses the favicon URL if provided in the service data
- **Domain Extraction**: Extracts the domain from the service URL to construct a favicon URL
- **Favicon Service**: Falls back to a favicon service (e.g., Google's favicon service)
- **Default Icon**: Uses a default icon when no favicon can be loaded
- **Caching**: Caches favicons to reduce network requests and improve performance

## Accessibility

The ServiceIcon implements the following accessibility features:

- Keyboard navigation and selection
- ARIA attributes for selection state
- High contrast visual indicators
- Screen reader support for service names and states

## Related Components

- [ServiceGrid](ServiceGrid.md) - Container component that displays multiple ServiceIcons
- [ServiceCard](ServiceCard.md) - Expanded view of service information
- [LabelBar](LabelBar.md) - Filtering system that affects which ServiceIcons are displayed

## Related Documentation

- [Service Model](../models/service.md)
- [Inventory Page](../pages/inventory.md)
- [Command Execution Flow](../flows/command-execution.md)
