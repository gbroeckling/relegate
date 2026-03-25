# Security Policy

## Supported versions

| Version | Supported |
|---------|-----------|
| Pre-release | Community testing |

## Reporting a vulnerability

**Do not open a public GitHub issue for security problems.**

1. Go to the [Security Advisories](https://github.com/gbroeckling/relegate/security/advisories) page.
2. Click **Report a vulnerability**.
3. Describe the issue, impact, and steps to reproduce.
4. Expect a response within **7 days**.
5. Credit will be given in the changelog (you may request anonymity).

## What counts as a security issue

- Credential leakage (passwords, API keys exposed in logs or config)
- Remote code execution via email content
- Man-in-the-middle vulnerabilities in TLS handling
- Service escalation or unauthorized access to the web dashboard
- Attachment handling that could execute arbitrary code

## What does not count

- Issues requiring local admin access (the service runs locally by design)
- Bugs without security impact

## Security posture

Relegate inherits the security architecture of [GideonMail](https://github.com/gbroeckling/gideonmail):

- **No telemetry** — no data sent anywhere except your configured services
- **Local only** — all processing happens on your machine
- **Credentials encrypted** via OS-level secure storage
- **Email HTML never rendered** — Relegate is headless, no browser context
- **8 security filters** scan every email from unknown senders
- **Web dashboard** (when available) binds to localhost only
