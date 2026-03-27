# Architecture

## Overview

GideonMail (and by extension Relegate) follows a single-process architecture
where the Electron main process handles everything: IMAP connectivity, SMTP
sending, AI triage, SMS alerts, Google Calendar integration, and security
filtering. There is no separate backend server -- the main process *is* the
backend.

Relegate will run the same engine as a headless Windows service, replacing the
Electron renderer with a web dashboard.

## File Structure

```
main.js            # Main process (~4000 lines) -- IMAP, SMTP, AI, SMS,
                   # Calendar, Security, all IPC handlers
preload.js         # IPC bridge -- exposes safe APIs to the renderer via
                   # contextBridge
renderer/          # UI -- HTML, CSS, and vanilla JS for the desktop app
security.js        # Security filter pipeline -- 8 filters for email scanning
google-auth.js     # Google OAuth2 flow for Calendar integration
package.json       # Dependencies and Electron config
```

### Why a single main.js?

Keeping all backend logic in one file simplifies debugging, searching, and
understanding the flow. Utility modules are broken out only when they serve a
clearly distinct purpose (security filtering, OAuth). This is a deliberate
architectural choice, not technical debt.

## Data Flow

```
IMAP Server
    |
    v
Fetch new emails (IMAP IDLE + polling)
    |
    v
Security filters (8-filter pipeline on unknown senders)
    |
    v
AI triage (Claude Haiku) -- categorize, extract intent, decide action
    |
    v
Act on results:
    +-- SMS alert (Textbelt) for urgent emails
    +-- Calendar event (Google Calendar) for meetings/deadlines
    +-- File into category (Important, FYI, Marketing, etc.)
    +-- Draft reply for review
    +-- Flag for human attention
    |
    v
Update UI / Send notifications
```

## IMAP Connection Management

IMAP is the most failure-prone part of the system. The architecture uses two
strategies:

- **Shared client** -- A persistent IMAP connection for IDLE monitoring and
  routine operations. This connection is kept alive and automatically
  reconnected on drops (ECONNRESET, timeout).
- **Fresh clients for parallel operations** -- When multiple operations need to
  run simultaneously (batch fetching, search + fetch, etc.), fresh IMAP clients
  are created to avoid lock contention on the shared connection. Each fresh
  client connects, performs its operation, and disconnects.

This hybrid approach balances connection efficiency with reliability.

## AI Integration

All AI calls go through **Claude Haiku** (fast, cost-effective):

- **Email triage** -- Classify incoming emails by urgency and category
- **Intent extraction** -- Determine what action (if any) the email requires
- **Chat interface** -- Users can ask questions about their email via a chat
  panel. The AI uses `tool_use` to perform actions (search emails, draft
  replies, check calendar) within the conversation.
- **Low Touch mode** -- Fully automated processing where the AI triages and
  acts on emails without user interaction

## Security Architecture

Security is enforced at multiple layers:

- **contextIsolation** -- The renderer runs in an isolated context with no
  direct access to Node.js APIs.
- **No nodeIntegration** -- Node.js is fully disabled in the renderer.
- **Sandboxed iframe** -- Email HTML is rendered inside a sandboxed iframe that
  cannot execute scripts, navigate, or access the parent frame.
- **8-filter pipeline** (`security.js`) -- Every email from unknown senders is
  scanned for:
  1. Phishing indicators
  2. Spoofed sender addresses
  3. Suspicious links
  4. Dangerous attachments
  5. Social engineering patterns
  6. Header anomalies
  7. Content red flags
  8. Composite threat scoring
- **Verification codes** -- Action emails include verification codes so users
  can confirm AI-initiated actions are legitimate.

## Storage

All data is stored locally using **electron-store**, which writes JSON files to
the user's app data directory. There is no database.

Stored data includes:
- Email account credentials (encrypted)
- API keys (encrypted)
- Sender categories and rules
- App settings and preferences
- AI triage history

## Relegate (Service Version)

Relegate will share the same core engine with these differences:

| | GideonMail | Relegate |
|---|---|---|
| Runtime | Electron | Windows service (node-windows) |
| UI | Electron renderer | Web dashboard (planned) |
| Process | Desktop app | Background service |
| Platform | Windows (Mac planned) | Windows |
| Status | Active development | Pre-release |

The service version strips out the renderer and runs the main process logic
as a long-lived background service. A localhost web dashboard is planned for
configuration and monitoring.
