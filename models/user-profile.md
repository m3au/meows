---
title: User Profile Model
description: User profile data model specification and implementation details
detail_level: Technical implementation details
tags: [models, data, user, profile]
revised: false
---

# User Profile Model

The User Profile model represents user account information and settings in meows.space. It contains personal information, authentication details, and references to user-specific data.

## Data Structure

```typescript
interface UserProfile {
  id: string; // Unique identifier
  email: string; // User email
  display_name: string; // Display name
  avatar_url?: string; // Profile picture URL
  created_at: string; // Account creation timestamp
  updated_at: string; // Last update timestamp
  last_login: string; // Last login timestamp

  // Account status
  status: "active" | "inactive" | "suspended";
  email_verified: boolean; // Email verification status

  // Subscription
  plan: "free" | "premium" | "team";
  plan_expires?: string; // Subscription expiration

  // Usage metrics
  command_count: number; // Number of commands
  execution_count: number; // Total command executions

  // References
  preference_id: string; // Reference to preferences
  active_workspace_id: string; // Active workspace
}
```

## Authentication

User authentication is handled through:

- Email/password authentication
- OAuth providers (Google, GitHub)
- JWT tokens for API access

## User Types

### Anonymous Users

Users who haven't created an account:

- Limited to local storage only
- No synchronization
- Basic functionality only

### Registered Users

Users with accounts:

- Cross-device synchronization
- Command sharing
- Full feature access

### Premium Users

Users with paid subscriptions:

- Advanced features
- Higher usage limits
- Priority support

## Workspaces

Users can have multiple workspaces, each with its own:

- Set of commands
- Labels and organization
- Default settings
- Usage context

## Storage and Synchronization

User profiles are stored in:

- **IndexedDB**: Basic profile info for offline access
- **Server Database**: Complete profile data

Profile data is synchronized across devices when the user is logged in.

## Privacy and Security

User data is protected through:

- Encrypted storage
- HTTPS transmission
- JWT authentication
- Permission-based access control

## Related Models

- [User Preferences Model](user-preferences.md) - For user settings
- [Command Model](command.md) - For user-created commands
- [Label Model](label.md) - For user-created labels

## Related Documentation

- [Settings Page](../pages/settings.md)
- Technical Implementation (Documentation moved)
- API Endpoints (Documentation moved)
