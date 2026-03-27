# Security Policy

## Supported Versions

| Version | Status | Supported |
|---------|--------|-----------|
| Relegate | Pre-release | Community testing |
| GideonMail 0.2.x | Current desktop app | Active development |

Relegate is in pre-release. Security issues found in the shared engine will be
fixed in both Relegate and GideonMail.

## Reporting a Vulnerability

**Do not open a public GitHub issue for security problems.**

1. Go to the [Security Advisories](https://github.com/gbroeckling/relegate/security/advisories) page.
2. Click **Report a vulnerability**.
3. Describe the issue, its impact, and steps to reproduce.
4. Expect acknowledgment within **7 days**.
5. Credit will be given in the changelog (you may request anonymity).

## What Counts as a Security Issue

- **XSS** -- Cross-site scripting via email content or rendered HTML
- **Injection** -- Code injection through email headers, bodies, or attachments
- **Auth bypass** -- Unauthorized access to the web dashboard or API endpoints
- **Credential exposure** -- Passwords, API keys, or tokens leaked in logs,
  config files, or error messages
- **IMAP credential leaks** -- Email credentials exposed through insecure
  storage, transmission, or logging

## What Does Not Count

- **Physical access attacks** -- The service runs locally by design; physical
  machine access is out of scope
- **Denial of service on localhost** -- Flooding the local service is not a
  meaningful attack vector
- **Non-security bugs** -- Crashes, UI glitches, or functional issues should be
  filed as regular bug reports
- **Social engineering** -- Phishing the user into providing credentials is not
  a software vulnerability

## Security Measures

Relegate inherits and extends the security architecture of
[GideonMail](https://github.com/gbroeckling/gideonmail):

- **No telemetry** -- No data is sent anywhere except your explicitly configured
  services (IMAP, SMTP, Claude API, Textbelt, Google Calendar).
- **No cloud sync** -- All processing happens entirely on your machine.
- **Local-only storage** -- Settings and data are stored locally using
  electron-store JSON files.
- **Encrypted credentials** -- Passwords and API keys are encrypted via
  OS-level secure storage.
- **Sandboxed HTML rendering** -- Email HTML is rendered in a sandboxed iframe
  with no access to the main process.
- **contextIsolation enabled** -- The renderer process cannot access Node.js
  APIs directly.
- **No nodeIntegration** -- Node.js is fully disabled in the renderer context.
- **8 security filters** -- Every email from unknown senders passes through an
  8-filter pipeline that scans for phishing, spoofing, suspicious links,
  dangerous attachments, and other threats.
- **Verification codes on action emails** -- When the AI takes action on an
  email (forwarding, replying), a verification code is included so you can
  confirm the action is legitimate.
