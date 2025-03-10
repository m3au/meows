---
title: User Model
description: User account data model specification
detail_level: Data structure
tags: [model, user, authentication, data]
---

# User Model

The User model represents core user account information in meows.space. It contains authentication details, account status, and references to associated data models.

## Schema

```typescript
interface User {
  id: string; // Unique identifier
  email: string; // User email address
  auth_provider: string; // Authentication provider
  auth_provider_id?: string; // External provider ID
  password_hash?: string; // Hashed password (if using email/password)

  // Account status
  is_verified: boolean; // Email verification status
  status: "active" | "inactive" | "pending_deletion";

  // Timestamps
  created_at: string; // Account creation timestamp
  updated_at: string; // Last update timestamp
  last_login: string; // Last login timestamp

  // References
  profile_id: string; // Reference to user profile
  active_catalog_id: string; // ID of the currently selected catalog/workspace
}
```

## Properties

| Property            | Type    | Description                                                       |
| ------------------- | ------- | ----------------------------------------------------------------- |
| `id`                | string  | Unique identifier for the user account                            |
| `email`             | string  | User's email address (unique)                                     |
| `auth_provider`     | string  | Authentication method ("local", "github", "google", etc.)         |
| `auth_provider_id`  | string  | ID from external auth provider (for OAuth)                        |
| `password_hash`     | string  | Bcrypt hash of password (only for local auth)                     |
| `is_verified`       | boolean | Whether email has been verified                                   |
| `status`            | string  | Account status (active, inactive, pending_deletion)               |
| `created_at`        | string  | ISO timestamp of account creation                                 |
| `updated_at`        | string  | ISO timestamp of last update                                      |
| `last_login`        | string  | ISO timestamp of last login                                       |
| `profile_id`        | string  | Reference to associated UserProfile                               |
| `active_catalog_id` | string  | Reference to the catalog/workspace currently selected by the user |

## Authentication Methods

The User model supports multiple authentication methods:

### Email/Password Authentication

For users who register with email and password:

- Email must be verified
- Password is stored as a bcrypt hash
- Password must meet strength requirements

### OAuth Authentication

For users who authenticate via external providers:

- Provider ID is stored for reference
- Email is typically pre-verified by provider
- No password is stored

## Account Lifecycle

The User model tracks the following account states:

1. **Creation**: Initial account creation with unverified status
2. **Verification**: Email verification to activate account
3. **Active**: Normal account operation
4. **Inactive**: Temporary suspension or dormancy
5. **Pending Deletion**: Grace period before permanent deletion
6. **Deleted**: Account data removed (not stored in database)

## Security Considerations

- Email addresses are stored in their original form but validated
- Passwords are never stored in plain text
- Authentication tokens are not stored in the User model
- Account status changes are logged for security auditing

## Related Models

- [User Profile](user-profile.md) - Contains user's profile information
- [Catalog](catalog.md) - User's command collections
- [User Preferences](user-preferences.md) - User's application settings

## Storage and Synchronization

User data is stored in:

- **Server Database**: Primary storage for authentication data
- **IndexedDB**: Minimal reference data for local operations

Authentication data is never synchronized to client storage in raw form.

## Related Documentation

- [Registration Flow](../flows/authentication-registration.md)
- [Login Flow](../flows/authentication-login.md)
- [Account Deletion Flow](../flows/account-deletion.md)
- Authentication Security (Documentation moved)
