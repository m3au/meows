---
title: Global Catalog Model
project: meows
description: Global Catalog data model specification
target: Developers
detail_level: Data structure
last_updated: 2024
tags: [model, global catalog, data, commands, discovery]
---

# Global Catalog Model

The Global Catalog model implements the shared, community-maintained collection of commands available to all users. It contains verified, popular commands that can be imported to a user's personal inventory.

## Schema

```typescript
interface GlobalCatalog {
  // Core properties
  commands: GlobalCatalogEntry[]; // Commands in the global catalog
  total_commands: number; // Total number of commands

  // Discovery metrics
  popularity_threshold: number; // Minimum popularity for featured status
  trending_commands: string[]; // IDs of currently trending commands
  featured_commands: string[]; // IDs of featured commands

  // Metadata
  last_updated: string; // Last update timestamp
  update_frequency: string; // How often the catalog is updated
}

interface GlobalCatalogEntry {
  command_id: string; // Reference to command
  popularity_score: number; // Calculated popularity score
  usage_count: number; // Total usage count
  average_rating: number; // Average user rating (1-5)
  rating_count: number; // Number of ratings
  verified: boolean; // Whether command is verified
  featured: boolean; // Whether command is featured
  trending_score: number; // Current trending score
  added_date: string; // When command was added to global catalog
}
```

## Properties

| Property               | Type                 | Description                                                  |
| ---------------------- | -------------------- | ------------------------------------------------------------ |
| `commands`             | GlobalCatalogEntry[] | Array of commands in the global catalog with metadata        |
| `total_commands`       | number               | Total number of commands in the catalog                      |
| `popularity_threshold` | number               | Minimum popularity score for a command to be featured        |
| `trending_commands`    | string[]             | IDs of commands currently trending                           |
| `featured_commands`    | string[]             | IDs of commands featured by the system                       |
| `last_updated`         | string               | ISO timestamp of last catalog update                         |
| `update_frequency`     | string               | How often the catalog is refreshed (e.g., "hourly", "daily") |

### GlobalCatalogEntry Properties

| Property           | Type    | Description                                                |
| ------------------ | ------- | ---------------------------------------------------------- |
| `command_id`       | string  | Reference to the command                                   |
| `popularity_score` | number  | Calculated score based on usage, ratings, and recency      |
| `usage_count`      | number  | Total number of times the command has been executed        |
| `average_rating`   | number  | Average user rating on a scale of 1-5                      |
| `rating_count`     | number  | Number of users who have rated the command                 |
| `verified`         | boolean | Whether the command has been verified by moderators        |
| `featured`         | boolean | Whether the command is featured in the catalog             |
| `trending_score`   | number  | Current trending score based on recent usage and ratings   |
| `added_date`       | string  | ISO timestamp when the command was added to global catalog |

## Usage

The Global Catalog serves as a discovery mechanism for users to find useful commands created by the community. It provides:

- A curated collection of high-quality commands
- Popularity metrics to help users find valuable commands
- Trending and featured sections to highlight noteworthy commands
- A source for users to import commands to their personal inventory

## Catalog Organization

The Global Catalog organizes commands in several ways:

### By Category

Commands are organized into categories based on their purpose or domain:

```text
[Development]
gh, npm, devdocs, stackoverflow, caniuse

[Media]
yt, spotify, netflix, imdb, soundcloud

[Knowledge]
wikipedia, wolfram, scholar, arxiv, pubmed
```

### By Popularity

Commands can be sorted by various popularity metrics:

- Star rating (highest to lowest)
- Usage count (most used)
- Trending score (current popularity)
- Recency (newest first)

### By Verification Status

Commands are classified by their verification status:

- **Verified**: Reviewed and approved by moderators
- **Community**: Created by users but not officially verified
- **Featured**: Highlighted by the system for quality or usefulness

## Catalog Operations

The system supports the following operations on the Global Catalog:

- **Browse**: View commands by category, popularity, or status
- **Search**: Find commands by keyword, functionality, or domain
- **Import**: Add commands from the global catalog to personal inventory
- **Rate**: Provide star ratings for commands
- **Report**: Flag inappropriate or broken commands
- **Suggest**: Submit commands for inclusion in the global catalog

## Data Collection and Privacy

The Global Catalog collects anonymous usage data to calculate popularity metrics:

- Command execution counts (anonymized)
- Star ratings from users
- Import frequency
- Search frequency

No personally identifiable information is stored with these metrics. Usage data is aggregated to protect user privacy.

## Related Models

- [[inventory|Inventory]] - User's personal collection of commands
- [[command|Command]] - Command structure and properties
- [[label|Label]] - Categories used to organize commands

## Related Documentation

- [[../pages/global-catalog|Global Catalog Page]]
- [[../components/CatalogView|Catalog View Component]]
- [[../components/CommandCard|Command Card Component]]
