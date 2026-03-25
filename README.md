# Relegate

### Put old email accounts on autopilot

**Beta: June 1, 2026**

You've got email accounts you don't check anymore — but they still matter. Business accounts from past ventures. Legacy addresses people still write to. Server admin mailboxes that get the one critical alert buried in 500 spam messages. They're too important to delete, too noisy to monitor.

**Relegate puts them on autopilot.** It connects to any IMAP account, runs AI triage on every incoming email, texts you when something actually matters, auto-files the rest, and keeps spam at bay — all in the background as a Windows service. No app to open. No inbox to check. Just a text when it counts.

> **Want to try the features now?** [GideonMail](https://github.com/gbroeckling/gideonmail) has every Relegate feature in a desktop email client you can test today.

---

## The Problem

Everyone has email accounts they've relegated to the background:

- The **business address** from a company you sold — clients still reach out
- The **admin mailbox** for your server that sends one critical alert per month buried in thousands of cron notifications
- The **old personal email** you gave to every store for 15 years — 99% spam, but your bank still uses it
- The **shared inbox** for a side project that occasionally gets a real customer
- The **ISPConfig/cPanel address** that catches everything on your domain

You can't delete them. You won't check them daily. You need something in between.

## The Solution

Relegate connects to these forgotten accounts and becomes their full-time manager:

- **AI reads every email** and decides: important, routine, or junk
- **Texts you** when something actually needs your attention
- **Auto-creates calendar events** from meeting requests
- **Blocks spam** with 8 security filters
- **Deletes known junk** after 7 days
- **Follows your rules** — teach it once, it handles the rest forever

Runs as a **Windows service**. Starts on boot. No window. No tray icon. Just quiet, reliable email management in the background.

---

## How It Works

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  Old IMAP    │────▶│   Relegate    │────▶│  Your Phone  │
│  Account     │     │  (service)   │     │  (SMS alert) │
└──────────────┘     │              │     └──────────────┘
                     │  AI triage   │
                     │  Spam filter │────▶ Google Calendar
                     │  Auto-file   │
                     │  Smart rules │────▶ Auto-delete junk
                     └──────────────┘
```

1. **Connect** — point Relegate at any IMAP account
2. **Configure** — set up your VIP senders, AI rules, and what triggers a text
3. **Forget** — Relegate handles the rest, forever

---

## Features

### Always-On Email Management
- Runs as a Windows service — starts on boot, runs silently
- Connects to any IMAP/SMTP server (ISPConfig, Dovecot, Postfix, Zimbra, cPanel)
- Check interval: 15 minutes to 24 hours
- No desktop UI required — pure background processing

### AI Triage (Claude)
- Every email analyzed for urgency and intent
- Standing instructions: teach it your rules once (e.g., "anything about invoices is urgent", "delete all newsletters except from HackerNews")
- Per-sender AI analysis with configurable actions
- Meeting detection with automatic calendar event creation

### Smart Sender Lists

| Role | What Relegate does |
|------|-------------------|
| **VIP** | Always texts you. Meetings auto-detected. Spam filters skipped. |
| **Watch** | AI analyzes every email. Configurable: SMS, auto-calendar, flag. |
| **Blocked** | Auto-deleted after 7 days. Always spam-filtered. Never texts. |
| **Muted** | No notifications. Spam filters skipped. Stays in inbox. |

### SMS Alerts
- VIP sender alerts with AI summaries
- "MEETING from Nicole: Dinner Friday 7pm"
- Conversation alerts: texts when active threads get replies
- Quiet hours, rate limits, batch mode
- Catches up on emails from while service was stopped

### Security Filters
8 layers protecting neglected inboxes from threats:
- SpamAssassin, Spamhaus, VirusTotal, Safe Browsing, PhishTank, AbuseIPDB, ClamAV, Bayesian learning

### Auto-Cleanup
- Blocked sender emails auto-deleted after 7 days
- Never sends duplicate alerts (persistent tracking)
- Config backup on every restart

---

## Perfect For

| Account Type | How Relegate helps |
|-------------|-------------------|
| **Old business email** | AI triages, texts you for real client inquiries, deletes the rest |
| **Server admin mailbox** | Filters thousands of cron emails, texts you for actual alerts |
| **Legacy personal email** | Blocks 15 years of accumulated spam, surfaces bank/government notices |
| **Shared project inbox** | Watches for real customers, ignores automated notifications |
| **Domain catch-all** | Security-scans everything, only texts you for human senders |

---

## Try the Features Today

Every Relegate feature is available **right now** in [GideonMail](https://github.com/gbroeckling/gideonmail) — a full desktop email client with the same AI engine, SMS alerts, calendar integration, and sender management.

```bash
git clone https://github.com/gbroeckling/gideonmail.git
cd gideonmail
npm install
npm start
```

GideonMail is the testing ground. Relegate is the production service.

---

## How It Compares

| | Relegate | GideonMail | Email Forwarding | Server-Side Rules |
|---|:---:|:---:|:---:|:---:|
| Runs without UI | ✅ | Tray icon | N/A | ✅ |
| AI triage | ✅ | ✅ | ❌ | ❌ |
| SMS alerts | ✅ | ✅ | ❌ | ❌ |
| Meeting detection | ✅ | ✅ | ❌ | ❌ |
| Calendar integration | ✅ | ✅ | ❌ | ❌ |
| 8 security filters | ✅ | ✅ | ❌ | SpamAssassin only |
| Smart sender lists | ✅ | ✅ | ❌ | Basic |
| Standing AI rules | ✅ | ✅ | ❌ | ❌ |
| Handles neglected accounts | ✅ | ❌ (needs app open) | Partial | ❌ |

---

## Roadmap

| Milestone | Target | Status |
|-----------|--------|--------|
| Feature development in GideonMail | Now | ✅ Available |
| Engine extraction | May 2026 | Planned |
| Windows service wrapper | May 2026 | Planned |
| Web dashboard | May 2026 | Planned |
| **Beta release** | **June 1, 2026** | **Planned** |
| Standalone .exe | June 2026 | Planned |
| Multi-account support | July 2026 | Planned |
| Linux systemd service | July 2026 | Planned |

---

## Stay Updated

- **Star this repo** to get release notifications
- **Watch** for beta access announcements
- **Try [GideonMail](https://github.com/gbroeckling/gideonmail)** now to test every feature

---

## Development

Built by **Garry Broeckling**. Implementation is AI-assisted using **Claude** by Anthropic — all architecture, product decisions, and testing are human-directed.

Relegate is the background-service sibling of [GideonMail](https://github.com/gbroeckling/gideonmail). Same engine, no desktop.

---

## License

MIT — see [LICENSE](LICENSE).

Copyright (c) 2026 Garry Broeckling.
