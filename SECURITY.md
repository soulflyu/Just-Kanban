# Security

## Self-Signed Certificate

Just Kanban is signed with a self-signed certificate rather than an
Apple Developer ID. This means:

- macOS shows a security warning on first launch
- The certificate is not verified by Apple
- Gatekeeper cannot confirm the developer's identity

This is the expected behavior for an application without Apple
Notarization. It does not indicate a security vulnerability in the
application itself.

## Verifying the Download

Each release includes SHA-256 checksums for all distribution files.
Before running a downloaded release, verify its integrity:

```bash
# Download the .sha256 file from the release page
# Compare checksums:
sha256sum -c JustKanban-vX.Y.Z.zip.sha256
```

If the checksum does not match, do not run the file and report it
as a security concern.

## Network Behavior

The application makes no network requests during normal operation.
There are no telemetry, analytics, crash reporting, or update-check
endpoints.

You can verify this:

```bash
# Check linked frameworks (no Network.framework expected)
otool -L "/Applications/Just Kanban.app/Contents/MacOS/JustKanban"

# Search binary strings for analytics/telemetry endpoints
strings "/Applications/Just Kanban.app/Contents/MacOS/JustKanban" \
  | grep -Ei "analytics|telemetry|crashlytics|firebase|sentry"
# (expected: no output)

# Monitor network activity while using the app
sudo lsof -i -P -n | grep -i kanban
# (expected: no entries during normal use)
```

The only URL referenced anywhere in the application is the public
GitHub repository link in the About panel. This URL is opened in
your default browser only when you click it.

## Reporting Security Issues

If you discover a security vulnerability, please report it privately:

Open a security advisory at:
https://github.com/soulflyu/Just-Kanban/security/advisories/new

Please include:

- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Any suggested fixes (optional)

We aim to respond within 48 hours and resolve critical issues promptly.
