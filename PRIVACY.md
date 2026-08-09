# Privacy Policy

**Last updated:** 2026-08-08

## TL;DR

Just Kanban does not collect, transmit, store, or have access to any
of your data. The application runs entirely on your Mac. There is no
telemetry, no analytics, no crash reporting, and no cloud sync.

## What we don't collect

- **No telemetry** — no usage statistics are sent anywhere
- **No analytics** — no tracking of features, sessions, or behavior
- **No crash reports** — crashes are not reported to anyone
- **No personal information** — no account, no email, no identifier
- **No content** — your boards, cards, descriptions, tags, attachments,
  and notes are never transmitted
- **No metadata** — no timestamps, IP addresses, device IDs, or
  fingerprints are collected
- **No third-party SDKs** — the application has zero external
  dependencies and includes no analytics frameworks
- **No cookies or trackers** — there is no web component

## What the app does on your Mac

- Stores your data locally in a SQLite database
- Creates automatic local backups (stored on your disk)
- Reads/writes files in standard macOS Application Support directory
- Optionally exports/imports database files when you choose

## Where your data lives

| Type | Location |
|---|---|
| Database | `~/Library/Application Support/Kanban/Kanban.sqlite` |
| Backups | `~/Library/Application Support/Kanban/Backups/` |
| Exports | Wherever you save them via File → Export |

The application has no access to anything outside these directories
during normal operation.

## Network activity

The application makes **zero network requests** during normal use.

The only network reference in the entire application is the GitHub
repository URL displayed in the About panel. This URL is opened in
your default browser **only when you click it** — the application
does not open it automatically.

## How to verify

You can confirm these claims yourself:

1. **Disconnect from the internet** — the app continues to work
   fully (create boards, cards, attachments, exports all work).
2. **Activity Monitor → Network tab** — sort by "Bytes Sent" while
   using the app; no entries related to Just Kanban should appear.
3. **Console.app** — search for "JustKanban"; no network-related
   log entries will be present.
4. **Little Snitch or Lulu** (third-party firewalls) — create rules
   blocking all outbound traffic for JustKanban; the app works
   normally.
5. **Inspect the binary**:
   ```bash
   strings "/Applications/Just Kanban.app/Contents/MacOS/JustKanban" \
     | grep -E "http|api|analytics|telemetry"
   ```
   No analytics or telemetry endpoints will be found.
6. **Inspect imports**:
   ```bash
   otool -L "/Applications/Just Kanban.app/Contents/MacOS/JustKanban"
   ```
   No networking frameworks (no `Network.framework`, no analytics
   libraries) will be linked.

## Updates

If anything changes about how the application handles data, this
document will be updated and a note added to the release notes.

## Contact

For privacy questions: open an issue at
https://github.com/soulflyu/Just-Kanban/issues
