---
name: Command Execution Flow
project: meows
description: Technical documentation of command execution process
target: Technical stakeholders
detail_level: Implementation details
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

# Command Execution Flow

This document describes the flow of command execution in meows.space, from user input to URL navigation.

## Flow Diagram

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
```

## Flow Description

1. **Initial Load**

   - User opens a new tab
   - meow.space loads
   - System determines profile type (Global/User)
   - Input field receives focus automatically

2. **User Interaction**

   - User can either:
     - Type text in the input field
     - Click a command icon in the grid

3. **Command Processing**

   - For typed input:
     - System checks if input matches a command/alias
     - If no match, uses default search service
     - If static command, executes directly
     - If dynamic command, builds URL with query
   - For clicked icons:
     - If input field empty, executes static command
     - If input field has text, uses as parameter

4. **URL Navigation**
   - System opens appropriate URL in new tab
   - Focus returns to meow.space input
   - Command is added to history

## Error Handling

- Invalid commands default to search
- Parameter validation occurs before URL generation
- Network errors display user notifications
- Focus always returns to input for quick recovery

## Performance Considerations

- Command matching uses prefix-based search
- URL templates are pre-compiled
- Command history uses LRU caching
- Icon grid loads progressively
