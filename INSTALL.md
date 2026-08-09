# Installation

## Requirements

- macOS 14 Sonoma or newer
- Apple Silicon or Intel processor

## Download

1. Go to [Releases](https://github.com/soulflyu/Just-Kanban/releases)
2. Download the archive for your architecture:
   - `JustKanban-vX.Y.Z-arm64.dmg` — Apple Silicon (M1+)
   - `JustKanban-vX.Y.Z-x86_64.dmg` — Intel Macs
3. Open the downloaded file (double-click)

## Install

1. Drag `Just Kanban.app` to your **Applications** folder
2. If prompted, click "Replace" to overwrite an older version

## First Launch

On first launch, macOS will show a security warning:

```
"Just Kanban" can't be opened because it is from an unidentified
developer.
```

This is expected. Follow these steps:

1. **Do not double-click** the app
2. **Right-click** (or Control-click) on `Just Kanban.app`
3. Select **Open** from the context menu
4. In the dialog, click **Open**

The app will launch. On subsequent launches, you can open it normally
by double-clicking.

## Alternative: xattr

If the right-click method doesn't work, you can remove the quarantine
attribute manually:

```bash
xattr -dr com.apple.quarantine "/Applications/Just Kanban.app"
```

Then double-click the app to launch.

## Verifying the Installation

To verify the app is installed correctly:

1. Open Activity Monitor
2. Search for "JustKanban" — the process should appear when running
3. Your data will be stored at:
   `~/Library/Application Support/Kanban/Kanban.sqlite`

## Uninstall

To remove Just Kanban completely:

1. Drag `Just Kanban.app` to Trash
2. Optionally remove your data:
   ```bash
   rm -rf ~/Library/Application\ Support/Kanban/
   ```
   This will delete all boards, cards, attachments, and backups.

## Updating

To update to a new version:

1. Download the new release from
   [Releases](https://github.com/soulflyu/Just-Kanban/releases)
2. Drag the new `Just Kanban.app` to Applications, replacing the old one
3. Your data is stored separately and will be preserved

There is no automatic update check — check Releases periodically for
new versions.
