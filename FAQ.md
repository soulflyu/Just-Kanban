# Frequently Asked Questions

## Privacy

### Does the developer see my data?

No. The developer has no technical ability to see your boards, cards,
attachments, tags, or any other content. The application:

- Runs entirely offline
- Stores all data locally in SQLite on your Mac
- Contains no telemetry, analytics, or crash-reporting code
- Has zero external dependencies and no third-party SDKs
- Makes no network requests during normal operation

You can verify this yourself — disconnect from the internet and the
app continues to work fully. See [PRIVACY.md](PRIVACY.md) for
step-by-step verification.

### Is there any cloud sync?

No. There is no iCloud sync, no remote backup, no account system.
Your data lives only on the Mac where Just Kanban is installed.

### Does the app needs an internet?

No. The app does not check for updates, ping any server, or contact
any external service on launch or during use.

## Installation

### Why does macOS show a security warning?

Just Kanban is signed with a self-signed certificate rather than an
Apple Developer ID (which costs $99/year and requires a business
entity). This means macOS cannot verify the developer's identity and
shows a warning.

To run the app: right-click `Just Kanban.app` → "Open" → click
"Open" in the dialog. After the first launch, you can open it normally.

### Can I run it without enabling Developer Mode?

Yes. After the first right-click → "Open", the app will launch normally.
You do not need to enable Developer Mode in System Settings.

### Does it work on Intel Macs?

Yes. The release includes builds for both Apple Silicon (M1/M2/M3+)
and Intel Macs.

### Does it work on macOS 13 or older?

No. Just Kanban requires macOS 14 Sonoma or newer due to SwiftUI
features used in the application.

## Data

### Where is my data stored?

Your data is stored locally at:
- `~/Library/Application Support/Kanban/Kanban.sqlite`

Automatic backups are stored at:
- `~/Library/Application Support/Kanban/Backups/`

### How do I back up my data?

Use File → Export Database (`⌥⌘E`) to save a full copy of your
database. This creates a standalone `.sqlite` file you can store
anywhere.

Automatic backups run every 15 minutes and on app quit, keeping the
last 5 backups.

### How do I transfer my data to another Mac?

1. On the source Mac: File → Export Database (`⌥⌘E`)
2. Copy the exported `.sqlite` file to the new Mac
3. On the new Mac: File → Import Database (`⌥⌘I`)

### Can I open my data in other apps?

Yes. The database is a standard SQLite file. You can open it with
any SQLite-compatible tool:

```bash
sqlite3 ~/Library/Application\ Support/Kanban/Kanban.sqlite
```

### How do I uninstall the app?

1. Drag `Just Kanban.app` to Trash
2. Optionally delete your data:
   ```bash
   rm -rf ~/Library/Application\ Support/Kanban/
   ```

## Updates

### How do I update the app?

Download the new release from
[GitHub Releases](https://github.com/soulflyu/Just-Kanban/releases),
replace the old `.app` in Applications, and run it. Your data is
stored separately and will be preserved.

There is no automatic update check.

### Will my data work with a newer version?

Yes. The database format is designed to be forward-compatible.
Export your data before major updates as a precaution.

## Future

### Will there be a paid version?

There are no immediate plans for monetization. The app will remain
free for the foreseeable future. If a paid version ever appears,
free features will not be removed.

### Will there be iOS or Android versions?

No current plans. The project focuses on macOS.

### Can I request a feature?

Yes. Open a feature request at
https://github.com/soulflyu/Just-Kanban/issues

## Troubleshooting

### The app doesn't launch after download

1. Make sure you're on macOS 14 or newer
2. Right-click the app → "Open" instead of double-clicking
3. Check System Settings → Privacy & Security → allow the app if blocked

### My data is gone after an update

Your data is stored separately from the app. Check:
- `~/Library/Application Support/Kanban/`

If the folder exists but the database is missing, restore from a
backup in `Kanban/Backups/`.
