# Data Format

Just Kanban stores all data in a standard SQLite database. You own your
data completely.

## File Locations

| Type | Path |
|---|---|
| Main database | `~/Library/Application Support/Kanban/Kanban.sqlite` |
| Automatic backups | `~/Library/Application Support/Kanban/Backups/` |
| Export (via menu) | User-selected location |

## Schema

The database uses Core Data with SQLite persistence. The schema is:

### Board
| Attribute | Type | Description |
|---|---|---|
| `id` | UUID | Unique identifier |
| `name` | String | Board name |
| `colorHex` | String? | Board color (hex, e.g. `#FF5733`) |
| `createdAt` | Date | Creation timestamp |
| `updatedAt` | Date | Last modification timestamp |
| `sortOrder` | Int64 | Display order |

### Column
| Attribute | Type | Description |
|---|---|---|
| `id` | UUID | Unique identifier |
| `name` | String | Column name |
| `sortOrder` | Int64 | Display order |
| `createdAt` | Date | Creation timestamp |
| `updatedAt` | Date | Last modification timestamp |
| `colorHex` | String? | Column color (hex) |
| `isCollapsed` | Bool | Column collapsed state |
| `isVisible` | Bool | Column visibility |
| `sortMode` | String | Sort mode ("manual", "date", "alpha") |
| `sortAscending` | Bool | Sort direction |

### Card
| Attribute | Type | Description |
|---|---|---|
| `id` | UUID | Unique identifier |
| `title` | String | Card title |
| `descriptionMD` | String? | Card description (Markdown) |
| `colorHex` | String? | Card color (hex) |
| `startDate` | Date? | Start date |
| `dueDate` | Date? | Due date |
| `createdAt` | Date | Creation timestamp |
| `updatedAt` | Date | Last modification timestamp |
| `sortOrder` | Int64 | Display order |

### Tag
| Attribute | Type | Description |
|---|---|---|
| `id` | UUID | Unique identifier |
| `name` | String | Tag name |
| `colorHex` | String? | Tag color (hex, nil = no color) |

### Attachment
| Attribute | Type | Description |
|---|---|---|
| `id` | UUID | Unique identifier |
| `filename` | String | Original filename |
| `mimeType` | String | MIME type (e.g. `image/png`) |
| `fileSize` | Int64 | Size in bytes |
| `data` | Data? | File content (stored in DB) |
| `thumbnail` | Data? | Thumbnail image (PNG) |
| `createdAt` | Date | Creation timestamp |

## Relationships

```
Board (1) ←→ (N) Column
Column (1) ←→ (N) Card
Card (1) ←→ (N) Tag
Card (1) ←→ (N) Attachment
Board (1) ←→ (N) Tag  (board-scoped tags)
```

## External Binary Storage

Large attachments (images, files) are stored in the database using
Core Data's `NSAllowsExternalBinaryDataStorage` flag. This means:

- Files up to a certain size are stored directly in SQLite
- Larger files may be stored externally by SQLite
- Both cases are handled automatically — no action needed

## Export Format

Exported databases are standard SQLite files. You can open them with:

```bash
# View tables
sqlite3 exported.sqlite ".tables"

# View schema
sqlite3 exported.sqlite ".schema"

# Read data
sqlite3 exported.sqlite "SELECT * FROM ZCARD LIMIT 5;"
```

Note: Core Data uses prefixed table names (`ZBOARD`, `ZCOLUMN`, etc.)
and stores dates as Unix timestamps. Use the Core Data model for
accurate interpretation.

## Import / Export

Export: `File → Export Database` (`⌥⌘E`)
Import: `File → Import Database` (`⌥⌘I`)

Import replaces the current database entirely. Back up your current
data before importing.

## Backup

Automatic backups run:

- Every 15 minutes (checkpoint + copy, no VACUUM)
- On app quit (checkpoint + VACUUM + copy)

Maximum 5 backups are kept in `~/Library/Application Support/Kanban/Backups/`
with naming pattern: `Kanban_yyyy-MM-dd_HH-mm.sqlite`
