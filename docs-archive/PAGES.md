---
name: PAGES
project: meows
description: Page structure, routing, and navigation flow of the application
target: Frontend developers and UX designers
detail_level: Page-level technical details and user flow
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

# Page Structure <!-- omit from toc -->

## Table of Contents <!-- omit from toc -->

- [Page Map](#page-map)
- [Core Pages](#core-pages)
  - [Main Search (/)](#main-search-)
  - [Personal Catalog (/personal)](#personal-catalog-personal)
  - [Global Catalog (/catalog)](#global-catalog-catalog)
  - [Settings (/settings)](#settings-settings)
- [Authentication](#authentication)
  - [Login (/auth/login)](#login-authlogin)
  - [Register (/auth/register)](#register-authregister)
- [Dynamic Routes](#dynamic-routes)
  - [Service Details (/service/\[id\])](#service-details-serviceid)
- [Data Loading](#data-loading)
  - [Infinite Scroll](#infinite-scroll)
  - [Real-time Updates](#real-time-updates)

## Page Map

```mermaid
graph TD
    A[Root] --> B[Main Search]
    A --> C[Personal]
    A --> D[Global]
    A --> E[Auth]

    B --> B1[Search Interface]

    C --> C1[Personal Catalog]
    C --> C2[Settings]

    D --> D1[Global Catalog]
    D --> D2[Service Details]

    E --> E1[Login]
    E --> E2[Register]
```

## Core Pages

### Main Search (/)

Landing page with primary search interface

- Instant search access
- Command execution
- Quick navigation

### Personal Catalog (/personal)

User's workspace

- Personal service collection
- Tag organization
- Usage history

### Global Catalog (/catalog)

Service discovery

- Community services
- Trending/Popular
- Service details

### Settings (/settings)

User preferences

- Search provider defaults
- UI preferences
- Tag management

## Authentication

### Login (/auth/login)

- Email/password
- OAuth providers:
  - GitHub
  - Google

### Register (/auth/register)

- Account creation
- Email verification
- Initial setup

## Dynamic Routes

### Service Details (/service/[id])

```typescript
type Params = {
  id: string; // Service identifier
};
```

- Service metadata
- Usage stats
- Related services

## Data Loading

### Infinite Scroll

- Virtual rendering for performance
- Load more trigger at scroll threshold
- Maintains scroll position
- Prefetches next batch

### Real-time Updates

- WebSocket for live updates
- Optimistic UI updates
- Background sync
- Error recovery
