---
name: Q&A
project: meows
description: Questions and answers to complete the system description
target: Project stakeholders
detail_level: System specification details
last_updated: 2024
ai_guidelines: |
  - Document only implemented features
  - Use precise technical language
  - No business jargon or buzzwords
  - No code generation
  - No feature speculation
  - Factual, direct tone
  - Don't touch the table of contents
---

# System Description Q&A

## Table of Contents

- [1. User Experience](#1-user-experience)
- [2. Command System](#2-command-system)
- [3. UI/UX Details](#3-uiux-details)
- [4. Data Organization](#4-data-organization)
- [5. System Behavior](#5-system-behavior)
- [6. Integration](#6-integration)
- [7. User Feedback Mechanisms](#7-user-feedback-mechanisms)
- [8. Required Pages Structure](#8-required-pages-structure)

## 1. User Experience

### 1.1 First-Time User Experience

1. What does a user see when they first visit meows.space?

   - Initial layout varies based on user authentication status
   - For first-time visitors (without account):
     - Top navigation bar with hamburger menu on the right
     - Menu contains privacy data and terms of use links
     - Main search input box with service selector
     - Categories section below the search
     - Icon grid display with popular services (sorted by popularity)
     - Global catalogue link
     - Page footer at the bottom
   - Default view shows:
     - "All" category/label selected
     - Search options ordered by popularity

2. Is there an onboarding tutorial or wizard?

   - No complex wizard implementation planned
   - Simple documentation approach:
     - About page with text and images explaining system usage
     - Potential future addition of joyride for advanced features

3. Are there pre-populated example commands for new users?

   - Yes, default configuration for non-logged-in users includes:
     - Default set of category tags for services
     - Google as the default search service
     - Pre-populated icon grid
     - Access to global catalog as if using a "global user" account
     - All default commands and services are immediately usable

4. How does a user create their first command?
   - Process starts from home page:
     - Edit icon available next to the grid
     - Clicking edit redirects to personal catalog
   - In personal catalog, users can:
     - Create new services
     - Define service properties:
       - Name
       - Search query
       - Dynamic/static setting
       - Favicon (automatically fetched from domain when possible)
     - Manage categories
     - Create new categories
     - Organize services within categories

### 1.2 Command Discovery

1. How do users discover available commands?

   - Through the Global catalog which offers:
     - Category-based navigation
     - Search functionality
     - Sorting options:
       - Most popular commands
       - Highest rated commands
     - Browse and explore functionality

2. Is there a search function for commands?

   - Yes, search functionality is available in:
     - Personal catalog: For user's own commands
     - Global catalog: For all available commands

3. How are commands organized for discovery?

   - Uses a label-based system similar to Gmail:
     - Categories and tags are essentially the same thing
     - Commands/services can have multiple labels
     - Services can appear in multiple categories
     - Visibility depends on active category selection
     - Flexible organization system allowing overlapping categorization

4. How are popular commands surfaced to users?
   - Through multiple discovery mechanisms:
     - Global Catalog sorting options:
       - Sort by star ratings
       - Sort by number of users (adoption rate in personal catalogs)
       - User voting system with stars
     - Default homepage:
       - Shows "All" category with services sorted by popularity
       - Popular services are immediately visible to new users

### 1.3 Error Handling

1. What happens when a command fails to execute?

   - System is primarily local-first, so command execution failures are minimal
   - Only potential errors are during command management:
     - Saving changes to backend
     - Updating command properties
     - Syncing between devices
   - These errors are displayed to user through UI notifications

2. How are invalid command parameters handled?

   - System uses raw string handling without validation
   - Parameters are passed directly to URL construction
   - No parameter validation or type checking
   - Service-specific handling happens at destination

3. What feedback does the user get during command execution?

   - Minimal feedback needed as system just generates and opens URLs
   - Visual feedback for:
     - Command click/activation
     - URL opening in new tab
     - Focus returning to meow.space

4. How are network errors communicated to users?
   - Only relevant for command management operations:
     - Saving changes
     - Syncing between devices
   - Simple notification system for sync/save status
   - No network dependency for basic command execution

## 2. Command System

### 2.1 Command Structure

1. What are the different types of commands supported?

   - System supports two fundamental types:

     1. Simple Commands (Static):

        - Basic structure: `<alias> → <URL>`
        - Examples:
          - `gm` → gmail.com
          - `yt` → youtube.com
          - `wk` → wikipedia.org
        - Just a shortcut/alias that maps directly to a fixed URL
        - No parameters needed

     2. Dynamic Commands (with Query):
        - Structure: `<alias> <parameters> → <URL with interpolation>`
        - Uses query builder during setup
        - Can have multiple placeholders for interpolation:
          - Single parameter example:
            - `gi cats` → searches Google Images for "cats"
          - Multiple parameters example:
            - Translator command might need:
              - Text to translate
              - Source language
              - Target language
        - Command setup includes defining:
          - Where each placeholder goes in the URL
          - How many parameters are needed
          - Order of parameters

2. Parameter Types and Rules:
   - Through a query builder system that defines:
     - Parameter placement in URL
     - Number of required parameters (1-5)
     - Parameter order
   - No built-in type validation
   - Raw string handling
   - Service-dependent escaping
3. Special Character Handling:

   - Escape Strategy:
     - Service-dependent escaping
     - Configurable per command
     - Part of URL query builder
     - Handles different service requirements

4. Command Limitations:

   - No limit on total commands per user
   - No limit on command name length
   - No limit on URL length (browser limits apply)

5. Common Use Cases:

   - Translation services (3 parameters):
     - Text to translate
     - Source language
     - Target language
   - Search services:
     - Search query
     - Optional filters
   - API calls:
     - Multiple parameters
     - Service-specific escaping

6. Technical Implementation:
   - URL Query Building:
     - Service-specific escaping
     - Parameter interpolation
     - Special character handling
     - No parameter validation
     - No type checking
   - Command Storage:
     - Unlimited commands per user
     - Efficient icon-based display
     - Quick access through labels

### 2.2 Command Templates

1. Template System:
   - URL Query Building:
     - Service-specific escaping
     - Parameter interpolation
     - Special character handling
     - No parameter validation
     - No type checking
   - Limitations:
     - Maximum 5 parameters
     - No default values supported
     - No built-in type validation

## 3. UI/UX Details

### 3.1 Command Display

1. View Types:

   - List View:
     - Simple list format
     - Shows command name and icon
     - Compact display
   - Grid View:
     - Icon-based display (5-icon style)
     - Shows command name
     - Each command card shows:
       - Command name
       - Labels attached
       - Public/private status
       - Parameter preview (if any)
     - Minimal visual footprint

2. Command Interaction:
   - Quick Actions:
     - Hover behavior:
       - Shows tooltip with additional info
       - Quick preview of command details
     - Right-click menu:
       - Properties option
       - Other contextual actions
   - Properties View:
     - Detailed command information
     - Full URL template
     - Label management
     - Parameter configuration

### 3.2 Command Organization

1. Label-Based System:

   - Core Concept:
     - Similar to Gmail's labeling system
     - Commands can have multiple labels
     - No folders - flat structure with label filtering
     - Labels are user-defined
   - Label Interface:
     - Location: Below search input box
     - Behavior:
       - Click label to filter commands
       - Multiple labels can be selected (AND operation)
       - Click again to deselect
     - Visual:
       - Shows label name
       - Shows command count per label
       - Selected labels are highlighted

2. Filtering Behavior:

   - No labels selected:
     - Shows all commands
   - Single label selected:
     - Shows commands with that label
   - Multiple labels selected:
     - Shows commands that have ALL selected labels

3. Label Management:

   - Label Operations:
     - Create:
       - User can create new labels anytime
       - Labels are private to user
     - Edit:
       - Rename labels
       - Delete labels (doesn't delete commands)
     - Apply:
       - Add/remove labels from commands
       - Batch label operations supported
   - Label Limitations:
     - Maximum labels per user: Unlimited
     - Maximum labels per command: Unlimited
     - Label name restrictions:
       - Max 50 characters
       - Alphanumeric + spaces
       - Case insensitive

4. Search Integration:

   - Label-aware search:
     - Search within labeled subset
     - Can combine text search with label filters
   - Search includes:
     - Command name
     - Command description
     - URL content
     - Label names

5. Key Features:
   - No nested organization (flat structure)
   - Multiple labels per command
   - Dynamic filtering
   - Flexible organization
   - Simple user interface
   - Quick access through labels

### 3.3 Command Builder and Testing

1. Command Builder Interface:

   - Builder screen components:
     - Command name input
     - URL template builder
     - Parameter configuration
     - Label assignment
     - Test button (play icon)
     - Save button
     - Privacy toggle (private/public)
   - Live Testing:
     - Test button (play icon) behavior:
       - Performs parameter interpolation
       - Applies configured escape strategy
       - Opens new tab with constructed URL
       - Allows immediate verification
     - Real-time feedback:
       - See exact URL construction
       - Verify parameter handling
       - Check escape strategy results

2. Testing Workflow:

   - During Construction:
     ```
     Build Command → Test → Adjust → Test → Save
     ```
     - Iterative testing while building
     - Immediate feedback loop
     - No save required for testing
     - Multiple test iterations supported
   - Test Process:
     - Enter sample parameters
     - Click play icon
     - New tab opens with constructed URL
     - Verify service behavior
     - Return to builder for adjustments

3. Testing Features:

   - URL Construction Preview:
     - Shows final URL structure
     - Displays parameter interpolation
     - Shows escape strategy results
     - Real-time updates
   - Parameter Testing:
     - Test with actual values
     - Verify special character handling
     - Check service response
     - Validate URL construction

4. Command Lifecycle:

   ```
   Build → Test → Save (as Private) → Additional Testing → Publish (Optional)
   ```

   - Status Changes:
     - New commands:
       - Always save as private first
       - Testing required before save
     - Saved commands:
       - Can be modified and retested
       - Privacy toggle available
       - Can be published when ready

5. Publishing Process:

   - Requirements:
     - Command must be saved
     - Command must be tested
     - Initially saved as private
   - Publishing Steps:
     - Toggle privacy setting to public
     - Confirmation required
     - Command appears in global catalog
     - Can be toggled back to private

6. Key Testing Principles:
   - Test before save requirement
   - Real-time URL preview
   - New tab testing
   - Private-first approach
   - Simple publish toggle
   - Iterative testing support

## 4. System Behavior

### 4.1 Command Flow

1. Command Execution Flow:

   ```mermaid
   flowchart TD
       Start([Open New Tab]) --> Load[meow.space loads]
       Load --> Profile{Profile Type}

       Profile -->|Global| LoadGlobal[Load Global Profile]
       Profile -->|User| LoadUser[Load User Profile]

       LoadGlobal --> Focus[Auto-focus Input]
       LoadUser --> Focus

       Focus --> UserAction{User Action}

       UserAction -->|Type Text| Input[Text in Input Field]
       UserAction -->|Click Command Icon| IconClick{Input Has Text?}

       Input -->|Press Enter| CheckInput{Is Command/Alias?}

       IconClick -->|No| Execute[Execute Static Command]
       IconClick -->|Yes| BuildURLFromIcon[Build Dynamic URL with Input Text]

       CheckInput -->|No Match| DefaultSearch[Search with Default Web Service]
       CheckInput -->|Static Command| Execute
       CheckInput -->|"Dynamic Command + Space + Query"| BuildURL[Build Dynamic URL with Query]

       BuildURL -->|"Use Command's URL Template"| OpenDynamic[Open Dynamic URL]
       BuildURLFromIcon -->|"Use Command's URL Template"| OpenDynamic
       Execute --> OpenURL[Open Static URL]
       DefaultSearch --> OpenURL[Open URL in New Tab]
       OpenDynamic --> Return
       OpenURL --> Return[Return Focus to meow.space]

       %% Styles
       classDef profile fill:#e3f2fd,stroke:#2196f3
       classDef action fill:#e8f5e9,stroke:#4caf50
       classDef search fill:#fff3e0,stroke:#ff9800
       classDef check fill:#f3e5f5,stroke:#9c27b0
       classDef dynamic fill:#fce4ec,stroke:#e91e63

       class LoadGlobal,LoadUser,Profile profile
       class Execute,UserAction action
       class DefaultSearch search
       class CheckInput,IconClick check
       class BuildURL,BuildURLFromIcon,OpenDynamic dynamic
   ```

### 4.2 Command Privacy

1. Privacy Levels:

   - Private (default):
     - Only visible in user's personal catalog
     - Not discoverable by others
     - Full control by owner
   - Public (opt-in):
     - Owner explicitly publishes command
     - Appears in global catalog
     - Others can fork it
     - Original remains under owner's control

2. Command Sharing Process:

   - Publishing process:
     - User marks command as public
     - Command becomes visible in global catalog
     - Original author attribution is preserved
   - Forking process:
     - Users can fork any public command
     - Fork creates independent copy in user's catalog
     - Fork can be private or public
     - Original command remains unchanged
     - Fork maintains reference to original command

3. Command Ownership Rules:

   - Original command:
     - Only owner can modify
     - Owner can unpublish at any time
     - Owner maintains full control
   - Forked commands:
     - Fork owner has full control of their fork
     - Changes to fork don't affect original
     - Original changes don't affect forks
     - Fork history maintains link to original

4. Version Tracking:
   - Original commands:
     - Track modification date
     - No version history needed
   - Forks:
     - Track original source
     - Track fork date
     - Track fork author

### 4.3 User Permissions

1. Permission Levels:

   - Anonymous users can:
     - View global catalog
     - Use any public command
     - Cannot save/modify commands
   - Registered users can:
     - Create personal catalog
     - Create private commands
     - Publish their commands
     - Fork public commands
     - Modify own commands
     - Control privacy of own commands

2. Command Discovery Rules:

   - Through search:
     - Only searches public commands
     - Personal catalog search includes private commands
   - Through browsing:
     - Global catalog shows only public commands
     - Personal catalog shows all user's commands
     - Clear indication of public/private status

3. Key System Principles:
   - Privacy-focused approach:
     - Commands private by default
     - Explicit publish action required
     - Clear ownership model
   - Fork-based sharing:
     - Public commands can be forked
     - Forks are independent
     - Original attribution preserved
   - Personal control:
     - Users control privacy of their commands
     - Can publish/unpublish at will
     - Full control over own commands
   - Clear boundaries:
     - No modification of others' commands
     - Fork for modifications
     - Clean separation of ownership

### 4.4 User Data Management

1. What user data is stored?

   - User Profile:

     - Username
     - Avatar (for displaying as service creator on cards)

   - User Preferences:

     - URL opening behavior (new tab vs current tab)
     - Theme settings:
       - System theme
       - Light mode
       - Dark mode

   - Organization:
     - Categories/Tags/Labels
       - List of user's labels
       - Order of labels on homepage
       - Services assigned to each label
   - Services:
     - Personal catalog of services
     - Label assignments for services

## 5. Integration

### 5.1 Authentication Integration

1. What authentication methods are supported?
   - OAuth-based login through:
     - GitHub
     - LinkedIn
     - Facebook
   - No direct username/password authentication
   - Authentication only needed for command management

### 5.2 System Integration

1. Local-First Architecture:

   - System runs primarily in browser
   - Local storage for command data
   - Sync only for command management
   - No external service dependencies

2. Browser Integration:

   - No browser extension support needed
   - No bookmark integration (potential future feature)
   - No browser history integration
   - Commands tracked locally in system

3. External Services:
   - No external service dependencies
   - System generates URLs only
   - No API limits or quotas
   - No service credentials needed

## 6. Future Development

### 6.1 Phase 2 Features

1. Multiple User Profiles

   - Enable users to create and manage multiple profiles under one account
   - Each profile maintains separate:
     - Command sets
     - User preferences
     - Settings

2. Social Features

   - Command sharing capabilities
   - Social interactions:
     - Like/favorite commands
     - Share commands with other users
   - Community engagement features

3. Terminal Mode
   - Alternative command-line interface
   - Power user features:
     - Quick command execution
     - Terminal-style input
     - Keyboard-focused navigation

### 6.2 Implementation Priority

1. Development Phases:
   - Phase 1: Core functionality with single profiles
   - Phase 2: Features will be implemented based on user feedback and usage patterns

## 7. User Feedback Mechanisms

### 7.1 Active Feedback Channels

1. In-app Feedback Form:

   - Accessible via hamburger menu → "Send Feedback"
   - Single form for all types of feedback:
     - Bug reports
     - Feature suggestions
     - General issues
   - Simple input box with feedback type selection
   - Similar to Google's feedback implementation

2. Rating System:
   - Users can rate services/commands
   - System collects usage statistics

### 7.2 Analytics & Monitoring

1. Google Analytics Integration:
   - Track user behavior patterns
   - Monitor feature usage statistics
   - Click tracking implementation
   - User flow analysis capabilities

### 7.3 Support Channel

1. Contact Management:
   - Single point of contact: contact@[domain]
   - Handles all types of inquiries:
     - Technical support
     - Legal questions
     - General information

## 8. Required Pages Structure

### 8.1 Main Navigation

1. Primary Pages:
   - Home
   - Dashboard
   - Commands
   - Settings

### 8.2 Footer/Legal Pages

1. Legal Documentation:

   - Terms of Service
   - Privacy Policy
   - Data Protection

2. Help & Support:

   - FAQ
   - Contact Information
   - Support Documentation

3. Feedback:
   - Universal Feedback Form

### 8.3 Access Points

1. Navigation Elements:
   - Top-right hamburger menu
   - Footer navigation
   - Main navigation bar

## Remaining Questions to Address

All sections have been addressed.
