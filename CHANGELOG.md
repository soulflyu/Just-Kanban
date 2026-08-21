# Changelog

All notable changes to Just Kanban are documented here.

## [1.1] — 2026-08-21

### Added

- Done column flag: mark any column as final via its ⋯ menu — cards in done columns no longer highlight overdue or future start dates (multiple columns can be marked per board)

### Fixed

- Cards due today are no longer shown as overdue after midnight (due dates are now compared by calendar day)
- Start → due date range pills now use semantic colors: red when overdue, orange when the card has not started yet

## [1.0.0] — 2026-08-08

### Added

- Initial public release
- Kanban board management (boards, columns, cards)
- Drag & drop for cards and columns
- Card details: title, description, color, start/due dates
- Tags with custom colors
- File attachments with thumbnail previews
- Card search across all boards
- Column visibility toggle and collapse
- Automatic local backups (every 15 minutes + on quit)
- Database export and import
- Dark mode support
- Interface size adjustment (4 presets)
- Self-signed certificate for macOS Gatekeeper
