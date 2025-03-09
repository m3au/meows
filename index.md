---
title: meows.space Documentation
project: meows
description: Technical documentation for the meows.space project
target: Technical stakeholders
detail_level: System overview
last_updated: 2024
tags: [overview, documentation, architecture]
---

Welcome to the meows.space documentation. This knowledge base contains detailed documentation for the meows.space URL command multiplexer project.

![meows.space logo](https://cdn.midjourney.com/ba85aca6-a44e-4edd-9a03-020bfdd3ba7e/0_2.png)

Table of Contents

- [Overview](#overview)
- [Core Concept](#core-concept)
- [System Architecture](#system-architecture)
- [Command System](#command-system)
  - [Command Types](#command-types)
    - [Static Commands](#static-commands)
    - [Dynamic Commands](#dynamic-commands)
  - [Command Processing Pipeline](#command-processing-pipeline)
  - [Command Execution](#command-execution)
- [Command Organization and Catalog](#command-organization-and-catalog)
  - [Global Catalog](#global-catalog)
  - [Personal Catalog](#personal-catalog)
  - [User Profiles](#user-profiles)
- [State Management](#state-management)
  - [State Architecture](#state-architecture)
  - [Runtime State](#runtime-state)
  - [Persistent State](#persistent-state)
- [Data Synchronization](#data-synchronization)
  - [Local-First Operations](#local-first-operations)
  - [System Flow](#system-flow)
- [Frontend Architecture](#frontend-architecture)
  - [Technical Implementation](#technical-implementation)
  - [Component Architecture](#component-architecture)
  - [Loading \& Performance](#loading--performance)
    - [Progressive Loading Strategy](#progressive-loading-strategy)
    - [Performance Optimization Techniques](#performance-optimization-techniques)
- [Backend Architecture](#backend-architecture)
  - [API Implementation](#api-implementation)
  - [Data Storage](#data-storage)
  - [Security Implementation](#security-implementation)
- [Artifacts](#artifacts)
  - [Documents](#documents)
  - [Flows](#flows)
  - [Data Models](#data-models)
  - [Pages](#pages)
  - [Components](#components)
  - [API Endpoints](#api-endpoints)

---

## Overview

meows.space is a URL command multiplexer that transforms text commands into parameterized URLs. The system implements a browser-based interface with a local-first architecture, enabling offline command management and online URL resolution.

Users define commands that expand to full URLs with optional parameters. For example, `g cats` expands to `google.com/search?q=cats`, and `gh profile` expands to `github.com/profile`.

The system features a graphical interface with a Windows 95-style icon grid and organization tools. The three-layer state management provides offline capabilities while maintaining cross-device synchronization. The architecture implements progressive loading and local-first operations for performance optimization.

---

## Core Concept

meows.space transforms text inputs into navigable URLs through predefined templates. The system processes user commands and converts them to structured URLs using either static mappings or dynamic parameter interpolation.

The browser-based execution enables direct navigation to destinations. Command management functions offline, while URL resolution requires network connectivity.

---

## System Architecture

```mermaid
graph TD
    User[User] --> |Inputs Command| Client[Browser Client]
    Client --> |Parses Input| Parser[Command Parser]
    Parser --> |Resolves Command| Generator[URL Generator]
    Generator --> |Creates URL| Navigation[Browser Navigation]
    Navigation --> |Opens URL| Destination[Web Destination]

    Client --> |Stores| LocalDB[IndexedDB]
    LocalDB <--> |Syncs| SyncEngine[Sync Engine]
    SyncEngine <--> |Communicates| API[API Server]
    API <--> |Persists| Database[Database]

    Client --> |Records| History[Command History]
    Client --> |Manages| Preferences[User Preferences]
```

meows.space transforms text inputs into parameterized URLs through a local-first architecture. The system operates as a command multiplexer with URL routing and command history management, enabling offline command management and online URL resolution.

---

## Command System

The command system forms the core of meows.space, transforming user text inputs into parameterized URLs through a structured pipeline. It processes raw text commands, identifies command patterns, extracts parameters, and constructs destination URLs based on predefined templates. This system enables users to quickly navigate to web destinations using shorthand commands rather than typing full URLs.

### Command Types

```mermaid
graph TD
    subgraph "Command Types"
        Static["Static Commands<br/><i>Direct URL mapping</i>"]
        Dynamic["Dynamic Commands<br/><i>Parameter interpolation</i>"]
    end

    subgraph "Examples"
        Static --- StaticEx["gh → github.com<br/>cal → calendar.google.com<br/>mail → gmail.com"]
        Dynamic --- DynamicEx["g {query} → google.com/search?q={query}<br/>gh {repo} → github.com/{repo}<br/>tr {from} {to} {text} → translate.google.com/?sl={from}&tl={to}&text={text}"]
    end
```

The system supports two fundamental command types:

#### Static Commands

Static commands provide direct URL mappings without parameters:

```text
gm → gmail.com
cal → calendar.com
docs → docs.google.com
```

These commands navigate directly to the specified URL when invoked, serving as shortcuts for frequently accessed destinations.

#### Dynamic Commands

Dynamic commands incorporate parameters into URL templates:

```text
# Search engines
g {query} → google.com/search?q={query}
yt {query} → youtube.com/results?search_query={query}
gh {query} → github.com/search?q={query}

# Direct navigation
gh/r {repo} → github.com/{repo}
npm {pkg} → npmjs.com/package/{pkg}
maps {loc} → google.com/maps/search/{loc}

# Multiple parameters
tr {from} {to} {text} → translate.google.com/?sl={from}&tl={to}&text={text}
```

These commands support multiple parameters with interpolation into the final URL.

### Command Processing Pipeline

```mermaid
flowchart LR
    A[Raw Input] --> B[Parsing & Tokenization]
    B --> C[Command Lookup]
    C --> D[Template Hydration]
    D --> F[Browser Navigation]
```

The pipeline processes commands through these stages:

1. **Input parsing and tokenization** - Breaks down raw input into tokens
2. **Command lookup and parameter extraction** - Matches tokens to commands
3. **URL template hydration** - Populates templates with parameters
4. **Browser navigation** - Performs the navigation operation

### Command Execution

When a user interacts with meows.space, the command execution process follows a natural flow from input to navigation:

```mermaid
flowchart TD
    Start([User Input]) --> InputType{Input Type}

    InputType -->|Text Command| ParseText[Parse Text Command]
    InputType -->|Icon Click| IconClick[Process Icon Selection]

    ParseText --> CommandType{Command Type}
    IconClick --> HasParams{Has Parameters?}

    HasParams -->|Yes| GetParams[Get Parameters from Input]
    HasParams -->|No| DirectURL[Use Direct URL]

    CommandType -->|Static| StaticResolve[Resolve Static URL]
    CommandType -->|Dynamic| DynamicResolve[Extract Parameters]

    DynamicResolve --> TemplateHydration[Hydrate URL Template]
    GetParams --> TemplateHydration

    StaticResolve --> OpenURL[Open URL in Browser]
    DirectURL --> OpenURL
    TemplateHydration --> OpenURL

    OpenURL --> End([Return Focus])
```

The user begins by either typing a command or clicking an icon in the grid. For text input, the system parses the command and identifies whether it's static or dynamic. Static commands immediately resolve to their target URL, while dynamic commands extract parameters from the input and interpolate them into the URL template.

When a user clicks an icon, the system checks if there's text in the input field that should be used as a parameter. If parameters are needed, they're extracted from the input; otherwise, the system uses the direct URL associated with the command.

Once the final URL is constructed, the browser opens it in a new tab, and focus returns to meows.space for the next command. This streamlined process allows users to quickly navigate to their desired destinations with minimal effort.

---

## Command Organization and Catalog

The system provides both global and personal command catalogs with a flexible organization system. Users can have multiple profiles, each with its own set of commands and labels.

### Global Catalog

The global catalog serves as a distributed registry for command discovery and sharing. It contains commands created and shared by the community:

```text
[Development]
gh, npm, devdocs, stackoverflow, caniuse

[Media]
yt, spotify, netflix, imdb, soundcloud

[Knowledge]
wikipedia, wolfram, scholar, arxiv, pubmed
```

The catalog collects anonymous usage data and incorporates a star-based rating system. Users can rate commands from one to five stars, helping others discover the most useful and reliable commands. These ratings, combined with usage statistics, determine the popularity sorting in the catalog.

Commands are organized by labels and can be sorted by:

- Star rating (highest to lowest)
- Popularity (most used)
- Recency (newest first)
- Alphabetically (A to Z)

### Personal Catalog

Each user has a personal catalog where they can create, customize, and organize their own commands. The personal catalog uses a label-based indexing system:

```text
[Search]
- Google {shortcut: "g"}
- YouTube {shortcut: "yt"}
- Wikipedia {shortcut: "wiki"}

[Development]
- MDN {url: "developer.mozilla.org"}
- DevDocs {url: "devdocs.io/{topic}"}
- GitHub {url: "github.com/{repo}"}
- npm {url: "npmjs.com/package/{pkg}"}
```

Each command is represented by an icon in the grid. These icons are either automatically fetched from the domain favicon or custom icons uploaded by the user. Below each icon is the command name, similar to desktop shortcuts in traditional operating systems.

The organization system uses a flat label structure where each command can have multiple labels. This design enables commands to appear in different contexts based on their categorization. For example, a GitHub search command might appear under both "Development" and "Search" labels.

### User Profiles

Users can create multiple profiles, each with its own:

- Set of commands (each profile has its own distinct commands)
- Active label (the currently selected label for filtering)
- Set of labels shown under the input field
- Default browser settings

Each profile functions as a separate workspace, allowing users to maintain different command sets for different contexts, such as work, personal, or specific projects. The same command cannot have different parameters across profiles - if a user needs a variation of a command, they must create a new command in that profile.

---

## State Management

```mermaid
graph TD
    A[App State] --> B[Runtime State]
    A --> C[Persistent State]

    B --> D[Command Context]
    B --> E[Search State]
    B --> F[Navigation State]

    C --> G[IndexedDB]
    C --> H[Local Storage]
```

The state management system handles data persistence and retrieval across different storage layers. It maintains application state during runtime and across sessions.

### State Architecture

The state architecture consists of two primary components: runtime state in memory and persistent state in IndexedDB. Runtime state provides fast access to frequently used data, while persistent state ensures data durability across sessions.

### Runtime State

Runtime state contains the active application context during a session:

- **Command context** maintains the currently active command and its parameters. This includes the command being edited or executed, along with any extracted parameters.
- **UI state** tracks the current interface configuration, including selected commands, active panels, search queries, and scroll positions.
- **Command history** keeps a record of recently executed commands in an LRU cache, enabling quick access to frequently used commands without database queries.
- **Search index** provides an in-memory structure for fast command lookup, using prefix-based searching and fuzzy matching algorithms.

### Persistent State

Persistent state maintains durable data across browser sessions:

- **Command definitions** store all user-defined commands, including their URLs, parameters, and metadata. This forms the core of the user's command library.
- **User profiles** contain user information, including display name, email, and authentication details.
- **User preferences** store interface settings, default behaviors, and personalization options that persist across sessions.
- **Command history** maintains a comprehensive log of executed commands with timestamps and execution contexts.
- **Organization structure** stores the folder hierarchy, labels, and categorization system for commands.
- **Pending changes** queue modifications made while offline, ensuring they're synchronized when connectivity is restored.

---

## Data Synchronization

The data synchronization system manages bidirectional data flow between client and server databases.

### Local-First Operations

```mermaid
sequenceDiagram
    participant U as User
    participant C as Client
    participant D as IndexedDB
    participant S as Server

    U->>C: Execute Command
    C->>D: Store History
    C->>S: Log Usage
    S-->>C: Sync State
```

The system handles two primary processes:

**Command Management Synchronization** uses a transaction-based approach. When users modify commands, the system first applies changes to the local IndexedDB, then queues them for server synchronization. Each change is timestamped and assigned a unique transaction ID. When online, the system transmits these changes to the server in batches. For concurrent edits from multiple devices, the system applies last-writer-wins conflict resolution, with special handling for structural conflicts like command deletion followed by modification.

**Command Execution** records command usage statistics. When a user executes a command, the system logs this event locally and, when online, transmits usage data to the server for analytics. The browser handles the actual URL navigation after command processing.

### System Flow

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant IndexedDB
    participant API
    participant Database

    User->>Browser: Edit/Create Command
    Browser->>IndexedDB: Store Changes
    Browser-->>User: Update UI

    Browser->>API: Sync Changes
    API->>Database: Update Commands
    Database-->>API: Sync Complete
    API-->>Browser: Sync Confirmed

    User->>Browser: Execute Command
    Browser->>Browser: Navigate to URL
```

This diagram shows the data flow during command management and execution. Command edits are immediately stored in IndexedDB and reflected in the UI. When online, changes are synchronized with the server. For command execution, the browser constructs the URL and performs navigation directly.

---

## Frontend Architecture

The frontend architecture implements a React-based single-page application with a focus on performance, offline capabilities, and responsive design.

### Technical Implementation

The frontend is built using:

- **React** for component-based UI development
- **TypeScript** for type safety and developer experience
- **CSS Modules** for component-scoped styling
- **IndexedDB** for client-side storage
- **Service Workers** for offline capabilities

### Component Architecture

The component architecture follows a hierarchical structure with:

- **Container Components**: Handle data fetching and state management
- **Presentational Components**: Focus on rendering UI elements
- **Hooks**: Encapsulate reusable logic and state management
- **Context Providers**: Manage global state and theme

For detailed information about components, see the [Components](#components) section.

### Loading & Performance

```mermaid
graph LR
    subgraph "Progressive Loading"
        direction TB
        Shell["Shell<br/><i>10KB</i>"]
        Core["Core<br/><i>50KB</i>"]
        GlobalData["Global Data<br/><i>100KB</i>"]
        UserData["User Data<br/><i>Variable</i>"]
    end

    subgraph "Lazy-loaded Features"
        direction TB
        Settings["Settings<br/><i>15KB</i>"]
        Catalog["Catalog<br/><i>15KB</i>"]
        Search["Search<br/><i>10KB</i>"]
        Sync["Sync<br/><i>20KB</i>"]
    end

    Shell --> Core
    Core --> GlobalData
    GlobalData --> UserData

    UserData -.-> Settings
    UserData -.-> Catalog
    UserData -.-> Search
    UserData -.-> Sync
```

The application implements a sequential loading strategy to reduce initial load time. Through progressive loading and code splitting, the system loads critical functionality first while deferring non-essential features.

#### Progressive Loading Strategy

The application loads in a defined sequence:

1. **Shell (10KB)** loads first, containing the HTML structure, critical CSS, and minimal JavaScript for command input. This initial payload loads in approximately 200ms on standard connections, providing immediate access to the command input field.

2. **Core (50KB)** loads second, including the command parser, state management system, and primary UI components. This enables basic command execution while additional components continue loading.

3. **Global Data (100KB)** loads third, containing the public command catalog, default templates, and system configuration. This data is cached and shared across users, allowing non-authenticated users to access public commands.

4. **User Data (Variable Size)** loads last for authenticated users, including personal commands, preferences, history, and folder structure.

#### Performance Optimization Techniques

The application implements multiple optimization techniques:

**Code Splitting** divides the application into separate chunks that load on demand. Features like settings, command catalog, search functionality, and synchronization components load only when accessed, reducing initial load time.

**Virtual Rendering** for grids and lists renders only visible items, maintaining consistent performance with large command sets. This uses windowed rendering that creates DOM elements only for items in the viewport.

**Bundle Optimization** includes tree-shaking to remove unused code, module deduplication to reduce redundancy, and critical CSS extraction. The delivery pipeline uses Brotli compression, cache control with ETags, and content-based versioning.

**Data Prefetching** loads data before user interaction, such as prefetching command details on hover or loading the next page of results before reaching the current page end.

**Caching Strategy** uses multiple storage mechanisms:

- Browser cache for static assets
- IndexedDB for command data and user preferences
- Memory cache for frequently accessed data
- Service worker for offline functionality

---

## Backend Architecture

### API Implementation

The backend implements a REST API with endpoints for:

- Command storage and retrieval
- User authentication
- Cross-device synchronization

API endpoints use standard HTTP methods and return JSON responses with appropriate status codes. Authentication uses session tokens with configurable expiration.

For detailed information about API endpoints, see the [API Endpoints](#api-endpoints) section.

### Data Storage

Data is stored in two layers:

- IndexedDB for local client-side persistence
- PostgreSQL for server-side storage

The database schema mirrors the data models with tables for commands, users, and usage data. Indexes are implemented on frequently queried fields to optimize read performance.

### Security Implementation

```mermaid
graph TD
    A[Security] --> B[Authentication]
    A --> C[Data Storage]

    B --> D[Session Tokens]
    C --> E[Encrypted Storage]
```

Authentication uses session-based tokens stored in HTTP-only cookies. User passwords are hashed using bcrypt with a work factor of 10. HTTPS is required for all API communications.

---

## Artifacts

### Documents

| Document                                                 | Description                                                                                          | Key Topics                                                                      |
| -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| **[[technical/architecture\|System Architecture]]**      | Detailed overview of the system's structural design, core components, and their interactions.        | Component architecture, data flow, state management, performance optimization   |
| **[[technical/technology\|Technical Implementation]]**   | In-depth documentation of the implementation technologies, patterns, and practices.                  | React implementation, TypeScript usage, build process, deployment strategy      |
| **[[technical/components\|Component Architecture]]**     | Specification of the UI component system, including composition patterns and state management.       | Component hierarchy, state management, styling approach, accessibility features |
| **[[technical/endpoints\|API Endpoints]]**               | Documentation of the API endpoints, request/response formats, and authentication requirements.       | REST endpoints, GraphQL schema, authentication, rate limiting, error handling   |
| **[[technical/system-integration\|System Integration]]** | Guidelines for integrating with external systems, including webhooks, extensions, and data exchange. | Extension points, webhook specifications, data formats, security considerations |

### Flows

| Flow                                                  | Description                                                                                                                      | Key Steps                                                                                   |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [[flows/command-execution\|Command Execution]]        | Traces the journey from user input to URL navigation, showing how commands are parsed, parameters extracted, and URLs generated. | Input parsing → Command lookup → Parameter extraction → URL generation → Browser navigation |
| [[flows/command-management\|Command Management]]      | Documents the creation, editing, and organization of commands, including validation, storage, and synchronization processes.     | Command creation → Validation → Storage → Synchronization → Organization                    |
| [[flows/user-interaction\|User Interaction Patterns]] | Illustrates common user workflows across different pages, highlighting interaction patterns and navigation flows.                | Search → Execute → Organize → Customize → Share                                             |

### Data Models

| Model                                         | Description                                                                                                                                                                     | Key Properties                          |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| [[models/command\|Command]]                   | Defines the structure of command objects, including static and dynamic variants. Commands connect user input to URL templates and manage parameter extraction.                  | id, key, url, type, params, metadata    |
| [[models/service\|Service]]                   | Represents service metadata including icons, descriptions, and usage statistics. Services provide the visual representation of commands in the UI.                              | id, name, icon, description, popularity |
| [[models/tag\|Tag]]                           | Implements the label-based organization system, allowing commands to be categorized and filtered. Tags can be applied to multiple commands and commands can have multiple tags. | id, name, color, commands               |
| [[models/user-profile\|User Profile]]         | Manages user account information, authentication state, and cross-device synchronization. Profiles store user-specific data and preferences.                                    | id, displayName, email, preferences     |
| [[models/user-preferences\|User Preferences]] | Stores user-specific settings including theme preferences, default behaviors, and interface configurations.                                                                     | theme, defaultBrowser, commandsPerPage  |
| [[models/error-response\|Error Response]]     | Defines the standardized format for API error responses across the system.                                                                                                      | code, message, details, status          |

### Pages

| Page                                             | Route                                               | Description                                                                                                             | Key Features                                                |
| ------------------------------------------------ | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| **[[pages/main-search\|Main Search]]**           | **/**                                               | Primary interface for command execution, featuring a prominent search bar and quick access to frequently used commands. | Command input, history, suggestions, quick execution        |
| **[[pages/personal-catalog\|Personal Catalog]]** | **/personal**                                       | User's workspace for managing personal commands, with organization tools and customization options.                     | Command grid, label filtering, drag-and-drop organization   |
| [[pages/settings\|Settings]]                     | &nbsp;&nbsp;&nbsp;&nbsp;/personal/settings          | Configuration interface for user preferences, appearance settings, and default behaviors.                               | Theme selection, display options, default settings          |
| [[pages/create-command\|Create Command]]         | &nbsp;&nbsp;&nbsp;&nbsp;/personal/command/create    | Form interface for creating new command templates with parameter configuration and validation.                          | Template builder, parameter editor, preview functionality   |
| [[pages/create-command\|Edit Command]]           | &nbsp;&nbsp;&nbsp;&nbsp;/personal/command/edit/[id] | Editing interface for existing commands, allowing modification of templates and parameters.                             | Template editing, parameter configuration, usage statistics |
| **[[pages/global-catalog\|Global Catalog]]**     | **/catalog**                                        | Discovery interface for community-shared commands, with filtering, sorting, and import capabilities.                    | Command discovery, popularity sorting, import functionality |
| [[pages/service-details\|Service Details]]       | &nbsp;&nbsp;&nbsp;&nbsp;/catalog/service/[id]       | Detailed view of a specific service or command, showing metadata, usage information, and related commands.              | Command details, usage statistics, related commands         |
| **Authentication**                               | **/auth**                                           | User authentication and registration flows, supporting both email/password and OAuth providers.                         | Login, registration, account management                     |
| [[pages/login\|Login]]                           | &nbsp;&nbsp;&nbsp;&nbsp;/auth/login                 | Authentication interface for existing users, with multiple login options and security features.                         | Email/password login, OAuth providers, security measures    |
| [[pages/register\|Register]]                     | &nbsp;&nbsp;&nbsp;&nbsp;/auth/register              | Registration interface for new users, with account creation and verification processes.                                 | Account creation, email verification, initial setup         |
| **[[pages/help\|Help]]**                         | **/help**                                           | User guidance with visual demonstrations and explanations of key features and workflows.                                | GIF demonstrations, feature explanations, usage tips        |
| **[[pages/about\|About]]**                       | **/about**                                          | Information about the project, team, and technology stack, with links to resources and documentation.                   | Project information, team details, technology overview      |
| **[[pages/feedback\|Feedback]]**                 | **/feedback**                                       | Interface for users to submit feedback, report issues, and suggest improvements.                                        | Feedback form, issue reporting, feature requests            |
| **[[pages/privacy-policy\|Privacy Policy]]**     | **/privacy**                                        | Legal information about data handling practices, user rights, and compliance measures.                                  | Data collection, user rights, security measures             |
| **[[pages/terms-of-use\|Terms of Use]]**         | **/terms**                                          | Legal terms governing the use of the service, user responsibilities, and limitations.                                   | Usage terms, user obligations, liability limitations        |

### Components

| Component                                     | Description                                                                                                                                  | Usage                                         |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| [[components/SearchBar\|SearchBar]]           | Primary command input with autocomplete and history. Processes user text input and triggers command execution.                               | Main Search, Personal Catalog, Global Catalog |
| [[components/ServiceGrid\|ServiceGrid]]       | Windows 95-style icon grid displaying commands as interactive tiles. Supports drag-and-drop organization and visual categorization.          | Main Search, Personal Catalog, Global Catalog |
| [[components/TagBar\|TagBar]]                 | Label-based filtering system allowing users to organize and filter commands by categories. Implements multi-select filtering with AND logic. | Personal Catalog, Global Catalog              |
| [[components/CommandBuilder\|CommandBuilder]] | Form interface for creating and editing command templates. Includes parameter configuration, validation, and preview functionality.          | Personal Catalog, Service Details             |

### API Endpoints

| Endpoint                    | Method | Description             | Cached   |
| --------------------------- | ------ | ----------------------- | -------- |
| `/api/auth/login`           | POST   | User login              | No       |
| `/api/auth/logout`          | POST   | User logout             | No       |
| `/api/auth/register`        | POST   | New user registration   | No       |
| `/api/auth/session`         | GET    | Get current session     | No       |
| `/api/auth/refresh`         | POST   | Refresh access token    | No       |
| `/api/services`             | GET    | List all services       | Yes (5m) |
| `/api/services/:id`         | GET    | Get service details     | No       |
| `/api/services`             | POST   | Create new service      | No       |
| `/api/services/:id`         | PUT    | Update service          | No       |
| `/api/services/:id`         | DELETE | Delete service          | No       |
| `/api/services/search`      | GET    | Search services         | No       |
| `/api/tags`                 | GET    | List all tags           | Yes (5m) |
| `/api/tags`                 | POST   | Create new tag          | No       |
| `/api/tags/:id`             | PUT    | Update tag              | No       |
| `/api/tags/:id`             | DELETE | Delete tag              | No       |
| `/api/tags/trending`        | GET    | Get trending tags       | No       |
| `/api/user/preferences`     | GET    | Get user preferences    | No       |
| `/api/user/preferences`     | PUT    | Update preferences      | No       |
| `/api/user/history`         | GET    | Get search history      | No       |
| `/api/user/history`         | DELETE | Clear history           | No       |
| `/api/user/favorites`       | GET    | Get favorite services   | No       |
| `/api/user/favorites/:id`   | POST   | Add to favorites        | No       |
| `/api/user/favorites/:id`   | DELETE | Remove from favorites   | No       |
| `/api/providers`            | GET    | List search providers   | Yes (1h) |
| `/api/providers/:id/search` | GET    | Execute provider search | No       |
| `/api/providers/default`    | GET    | Get default provider    | No       |
| `/api/providers/default`    | PUT    | Set default provider    | No       |
| `/api/analytics/event`      | POST   | Log user event          | No       |
| `/api/analytics/trending`   | GET    | Get trending services   | Yes (1h) |
| `/api/analytics/popular`    | GET    | Get popular services    | No       |
| `/api/analytics/metrics`    | GET    | Get usage metrics       | No       |
