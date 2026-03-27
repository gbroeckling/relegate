# Relegate

### You can't delete it. You won't check it. Relegate it.

Relegate is a background Windows service that manages your forgotten email accounts on autopilot using AI. It connects to any IMAP account, triages every incoming message with Claude, texts you when something actually matters, handles the rest automatically, and keeps threats at bay — all without opening an app, checking an inbox, or lifting a finger.

---

<!-- Badges -->
<p>
  <img src="https://img.shields.io/badge/Beta-June%201%2C%202026-blue?style=flat-square" alt="Beta: June 1, 2026" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License" />
  <img src="https://img.shields.io/badge/Built%20with-Claude%20by%20Anthropic-blueviolet?style=flat-square" alt="Built with Claude" />
  <img src="https://img.shields.io/badge/Try%20Now-GideonMail-orange?style=flat-square" alt="Try GideonMail Now" />
</p>

> **Want to try every feature right now?** [GideonMail](https://github.com/gbroeckling/gideonmail) is the desktop version with the same AI engine, SMS alerts, calendar integration, sender management, and security filters — available today. Clone it, run it, see what Relegate will do for you.

---

## The Problem

You have email accounts you don't check anymore. Everyone does.

The **business address** from a company you sold three years ago — clients still write to it. The **server admin mailbox** that receives one critical security alert per month, buried under thousands of cron notifications. The **old personal email** you gave to every store, every signup form, every loyalty program for 15 years — it's 99% noise, but your bank still uses it. The **shared inbox** for a side project that gets a real customer inquiry once a month. The **catch-all address** on your domain that collects everything.

You can't delete these accounts. Important things still arrive. But you won't check them — not daily, not weekly, probably not at all until something goes wrong. They sit there, accumulating spam, missing real messages, and becoming security liabilities.

And even your **main** inbox has gaps that no email client fills:

- You tell a client "I'll send the proposal by Friday" — and **no email client tracks that promise**. You forget. They follow up. You look unreliable.
- Someone emails you "Let's meet Thursday at Starbucks" — and **no email client puts that on your calendar**. Not from the body of an email. Not from a casual message. Only from formal .ics invites that half the world doesn't use.
- You delete 15 emails a week from the same vendor — and **no email client notices the pattern** and offers to block them for you. You just keep deleting.
- A newsletter you subscribed to in 2019 sends you 3 emails a week — and **no email client unsubscribes for you**. The unsubscribe link is right there. Nobody clicks it.
- An important thread you've been active in gets a reply — and **no email client texts you about it**. It sits in your inbox until you happen to check.
- You need to reply to something but you're on your phone at the grocery store — and **no email client drafts a reply that sounds like you** and lets you send it with one tap.

Every email client assumes you're sitting at your desk, reading email. **Relegate assumes you're not.**

---

## The Solution

Relegate connects to your forgotten email accounts and becomes their full-time manager.

It runs as a **Windows service** — starts on boot, runs silently in the background, no window, no tray icon. Every few minutes, it checks your neglected accounts. AI reads every incoming message, decides what it means, and takes action:

- **Important?** You get a text. With a summary. And the meeting link, if there is one.
- **Needs a reply?** AI drafts one in your voice, sends it to your phone for one-tap approval.
- **Meeting request?** It's already on your calendar.
- **Newsletter?** Unsubscribed. Filed. Gone.
- **Spam?** Scanned by 8 security filters and deleted.
- **Routine notification?** Batched into a morning digest.

You teach it once. It handles everything forever. Set it up on a Saturday morning, and never think about those accounts again.

---

## How It Works

```
                        ┌─────────────────────────────────────────┐
                        │              R E L E G A T E             │
                        │          (Background Service)            │
┌──────────────┐        │                                         │        ┌──────────────────┐
│  Old IMAP    │───────▶│  ┌───────────┐    ┌──────────────────┐  │───────▶│  Your Phone      │
│  Account #1  │        │  │ 8-Layer   │    │ AI Triage        │  │  SMS   │  (text alerts +  │
├──────────────┤        │  │ Security  │───▶│ (Claude)         │  │        │   action emails) │
│  Old IMAP    │───────▶│  │ Filters   │    │                  │  │        └──────────────────┘
│  Account #2  │        │  └───────────┘    │ • Read & score   │  │
├──────────────┤        │                   │ • Summarize      │  │        ┌──────────────────┐
│  Old IMAP    │───────▶│                   │ • Draft replies  │  │───────▶│  Google Calendar  │
│  Account #3  │        │                   │ • Detect meetings│  │  OAuth │  (auto-schedule,  │
└──────────────┘        │                   │ • Track commits  │  │        │   conflict detect) │
                        │                   └──────────────────┘  │        └──────────────────┘
                        │                          │              │
                        │                    ┌─────┴──────┐       │        ┌──────────────────┐
                        │                    │ Auto-Pilot │       │───────▶│  Your Inbox       │
                        │                    │ Engine     │       │ SMTP   │  (digest emails,  │
                        │                    │ • File     │       │        │   action relays)  │
                        │                    │ • Delete   │       │        └──────────────────┘
                        │                    │ • Reply    │       │
                        │                    │ • Unsub    │       │
                        │                    │ • Nudge    │       │
                        │                    └────────────┘       │
                        └─────────────────────────────────────────┘
```

**Three steps, then you're done:**

1. **Connect** — point Relegate at any IMAP account
2. **Configure** — set up your VIP senders, standing instructions, and what triggers a text
3. **Forget** — Relegate handles the rest, permanently

---

## Features

### AI Email Triage

Powered by Claude (Anthropic), the AI engine reads every incoming email and makes intelligent decisions — not keyword matching, real comprehension.

- **Urgency scoring** — AI classifies every email as urgent, normal, or skip
- **Smart one-line summaries** — for SMS alerts and digest emails
- **Standing instructions** — persistent rules you teach once ("always flag emails from my accountant", "delete anything from noreply addresses", "anything mentioning invoices is urgent")
- **Voice learning** — AI samples your sent emails to learn your writing style, then drafts replies that sound like you wrote them
- **Thread summarization** — long email chains condensed to 1-2 sentences so you get the context without reading 47 replies
- **Per-sender AI analysis** — Watch list senders get full AI treatment on every message

**Cost:** ~$0.003 per email analyzed. $5 of Anthropic API credit lasts months for a neglected account.

### Low Touch Autopilot `EXPERIMENTAL`

Fully autonomous email processing. No app interaction needed — Relegate handles everything, asks for approval via your phone when needed.

- **Auto-categorize** — AI sorts every email: spam, newsletter, receipt, notification, action-required, meeting, deadline
- **Auto-file** — moves categorized emails to Newsletters/, Receipts/, Notifications/ folders
- **Auto-draft** — AI writes replies in your learned voice, sends to your phone for one-tap approval
- **Auto-unsubscribe** — detects newsletters with List-Unsubscribe headers and unsubscribes automatically (mailto and HTTP one-click)
- **Auto-nudge** — when your sent emails go unanswered for N days, sends a polite follow-up in your voice
- **Auto-schedule** — creates calendar events with AI-extracted date, time, and location

### Smart Sender Management

One unified **People** list where every sender gets a role. The role determines exactly how Relegate treats their messages.

| Role | What Relegate Does |
|------|-------------------|
| **VIP** | Always texts you. Meetings auto-detected and scheduled. Spam filters skipped. Top priority. |
| **Watch** | AI analyzes every email. Configurable: SMS alerts, auto-calendar, flag for review. |
| **Daily Update** | Batched into your morning briefing digest. No individual notifications. |
| **Blocked** | Auto-deleted after 7 days. Always spam-filtered. Never notifies you. |
| **Muted** | No notifications. Spam filters skipped. Stays in inbox untouched. |

Relegate's **Sender Reputation Learning** tracks how you interact with each sender over time — which ones you open, reply to, or delete — and suggests role changes. That vendor you always ignore? Relegate will suggest moving them to Muted. That address you suddenly started replying to? It'll suggest Watch or VIP.

### SMS Notifications

Real-time text alerts via Textbelt when something actually matters — delivered to your phone, not buried in another app.

- **VIP alerts** with AI-generated summaries
- **Meeting detection** — "MEETING from Nicole: Dinner Friday 7pm" with the Zoom/Teams/Meet link right in the text
- **Conversation alerts** — texts when active threads you've participated in get new replies
- **Quiet hours** — no texts between 10pm and 7am (configurable)
- **Rate limiting and batching** — never spams your phone
- **Catch-up mode** — when the service restarts, reviews what arrived while it was stopped

**Cost:** Textbelt is $10 for 1,000 texts. For a neglected email account, that's a year or more.

### Action Email Relay

Control your old email accounts from your phone without opening any app — through specially crafted action emails sent to your main inbox.

- **Branded HTML action emails** with one-tap buttons: Approve, Decline, Reply, Later, Ignore
- **Security-coded** — every action email contains a unique 12-character verification token
- **Tamper-proof** — replies without a valid security code are rejected
- **Auto-cleanup** — processed action emails delete themselves from your inbox
- **Phone-based replies** — tap "Send This Reply" to dispatch the AI-drafted response

### Google Calendar Integration

Relegate ensures you never miss a meeting from an account you don't check.

- **Auto-creates events** from VIP and Watch sender emails
- **ICS attachment parsing** — reads text/calendar parts and .ics files for accurate VEVENT data
- **Online meeting link extraction** — Zoom, Teams, Meet, and Webex URLs added to event description
- **Incomplete info handling** — AI constructs full join URLs from partial meeting IDs ("Zoom ID: 123 456 7890" becomes a clickable link)
- **Reschedule detection** — when the same sender updates a meeting, the existing event moves instead of creating a duplicate
- **Conflict detection** — checks your calendar before scheduling
- **Permanent OAuth** — stays connected via refresh tokens, no re-auth needed

### Smart Digest Email

A daily HTML digest email delivered to your main inbox every morning — your briefing on everything that happened across your neglected accounts.

- **AI-powered summaries** of every email received in the last 24 hours
- **Grouped by account and priority** — VIP messages first, then Watch, then routine
- **Commitment tracking callouts** — reminds you of promises you made that are coming due
- **Reputation change suggestions** — "You've deleted the last 12 emails from marketing@vendor.com. Move to Blocked?"
- **One clean email** instead of checking five forgotten inboxes

### Sender Reputation Learning

Relegate watches how you interact with senders over time and gets smarter about managing them.

- **Tracks opens, replies, and deletes** per sender across all managed accounts
- **Builds engagement scores** — knows which senders you care about and which you ignore
- **Suggests role changes** — promotes engaged senders to Watch/VIP, demotes ignored ones to Muted/Blocked
- **Learns passively** — no manual training needed, just use your email normally

### Commitment Tracking

Relegate scans your outgoing emails for promises and commitments, then makes sure you follow through.

- **AI-detected commitments** — "I'll send that report by Friday", "Let me get back to you next week"
- **Deadline extraction** — identifies when commitments are due
- **Nudges before deadlines** — reminds you via SMS or digest before a promise expires
- **Included in daily digest** — upcoming commitments highlighted in your morning briefing

### Security Filters

Eight scanning layers protect neglected inboxes from the threats that accumulate when nobody's watching.

| Layer | What It Does | Cost |
|-------|-------------|------|
| **SpamAssassin** | Reads server-side spam scores | Free |
| **Spamhaus ZEN** | DNS blocklist lookup | Free |
| **VirusTotal** | URL scanning with 70+ engines | Free (500/day) |
| **Google Safe Browsing** | URL threat detection | Free (10k/day) |
| **PhishTank** | Known phishing URL database | Free |
| **AbuseIPDB** | IP reputation scoring | Free (1k/day) |
| **ClamAV** | Local antivirus scanning | Free |
| **Bayesian Filter** | Learns spam patterns over time | Free |

VIP, Watch, and Muted senders bypass spam filters — you've already told Relegate they're safe.

### Daily Update Groups

Batch noisy-but-useful senders into a single morning briefing instead of individual notifications.

- **Assign senders the Daily Update role** — newsletters, monitoring alerts, project notifications
- **AI summarizes each email** in the group
- **Delivered as one digest section** in your morning briefing email
- **No SMS, no individual alerts** — just a clean summary once per day

---

## How It Compares

| | Relegate | GideonMail | Email Forwarding | Server-Side Rules |
|---|:---:|:---:|:---:|:---:|
| Runs without a UI | **Background service** | Desktop tray app | N/A | ✅ |
| AI email triage | ✅ | ✅ | ❌ | ❌ |
| Learns your writing voice | ✅ | ✅ | ❌ | ❌ |
| Auto-draft replies | ✅ | ✅ | ❌ | ❌ |
| Auto-unsubscribe | ✅ | ✅ | ❌ | ❌ |
| Auto-nudge follow-ups | ✅ | ✅ | ❌ | ❌ |
| SMS alerts with meeting links | ✅ | ✅ | ❌ | ❌ |
| ICS / calendar invite parsing | ✅ | ✅ | ❌ | ❌ |
| Reschedule + conflict detection | ✅ | ✅ | ❌ | ❌ |
| Google Calendar integration | ✅ | ✅ | ❌ | ❌ |
| 8-layer security filters | ✅ | ✅ | ❌ | SpamAssassin only |
| Smart sender roles (5 roles) | ✅ | ✅ | ❌ | Basic allow/deny |
| Standing AI instructions | ✅ | ✅ | ❌ | ❌ |
| Action email relay | ✅ | ✅ | ❌ | ❌ |
| Thread summarization | ✅ | ✅ | ❌ | ❌ |
| Sender reputation learning | ✅ | ✅ | ❌ | ❌ |
| Commitment tracking | ✅ | ✅ | ❌ | ❌ |
| Daily digest email | ✅ | ✅ | ❌ | ❌ |
| Daily Update sender groups | ✅ | ✅ | ❌ | ❌ |
| Handles neglected accounts | ✅ | ❌ (needs app open) | Partial | ❌ |

**GideonMail** is the lite/testing version — same features, desktop UI. **Relegate** is the production background service.

---

## Perfect For

| Account Type | How Relegate Helps |
|-------------|-------------------|
| **Old business email** | AI triages every message, texts you for real client inquiries, auto-drafts replies in your voice, deletes the rest |
| **Server admin mailbox** | Filters thousands of cron/monitoring emails, texts you only for actual alerts, batches the rest into a daily digest |
| **Legacy personal email** | Blocks 15 years of accumulated spam with 8 security filters, surfaces bank and government notices via SMS |
| **Shared project inbox** | Watches for real customer inquiries, auto-categorizes notifications, nudges you when replies are overdue |
| **Domain catch-all** | Security-scans everything that arrives, only texts you for messages from real humans, auto-deletes the noise |

---

## Try It Today

Every Relegate feature is available **right now** in [GideonMail](https://github.com/gbroeckling/gideonmail) — a full desktop email client with the same AI engine, SMS alerts, calendar integration, sender management, autopilot features, and security filters. GideonMail is the testing ground. Relegate is the production service.

```bash
git clone https://github.com/gbroeckling/gideonmail.git
cd gideonmail
npm install
npm start
```

Set up an account, add some VIP senders, enable AI triage, and see what it does. Everything you configure in GideonMail maps directly to how Relegate will work as a background service.

---

## Roadmap

| Milestone | Target | Status |
|-----------|--------|--------|
| Feature development in GideonMail | Now | ✅ Available |
| Engine extraction | May 2026 | Planned |
| Windows service wrapper | May 2026 | Planned |
| Web dashboard (localhost) | May 2026 | Planned |
| **Beta release** | **June 1, 2026** | **Planned** |
| Standalone `.exe` installer | June 2026 | Planned |
| Multi-account support | July 2026 | Planned |
| Linux `systemd` service | July 2026 | Planned |

---

## Requirements

**Required:**

- Node.js 18+
- IMAP/SMTP email account(s)
- Windows 10 or Windows 11

**Optional (bring your own API keys):**

| Service | What It Enables | Cost |
|---------|----------------|------|
| [Anthropic API](https://console.anthropic.com) | AI triage, summaries, drafting, categorization | ~$0.003/email |
| [Textbelt](https://textbelt.com) | SMS notifications | $10 / 1,000 texts |
| [Google Calendar](https://console.cloud.google.com) | Auto-scheduling, conflict detection | Free |
| [VirusTotal](https://www.virustotal.com) | URL scanning (70+ engines) | Free (500/day) |
| [AbuseIPDB](https://www.abuseipdb.com) | IP reputation checking | Free (1k/day) |

---

## Documentation

| Guide | Description |
|-------|-------------|
| [Features](docs/FEATURES.md) | Complete feature reference — every feature with how it works and why it matters |
| [Architecture](docs/ARCHITECTURE.md) | Technical design: data flow, IMAP management, AI integration, security model |
| [API Setup](docs/API-SETUP.md) | Step-by-step setup for Anthropic, Textbelt, Google Calendar, and security APIs |
| [Troubleshooting](docs/TROUBLESHOOTING.md) | Common issues and solutions: IMAP, SMS, calendar, Low Touch |
| [Marketing](docs/MARKETING.md) | Positioning, target audience, competitive analysis, and launch plan |

---

## Stay Updated

- **[Star this repo](https://github.com/gbroeckling/relegate)** to get release notifications when beta drops
- **Watch** for beta access announcements and progress updates
- **[Try GideonMail](https://github.com/gbroeckling/gideonmail)** right now to test every feature in a desktop client

---

## Development

Relegate is built by **[Garry Broeckling](https://github.com/gbroeckling)** — a 30+ year coding veteran who ships fast with strong opinions. All architecture, product decisions, testing, and releases are human-directed. Implementation is AI-assisted using **[Claude](https://claude.ai) by Anthropic**, which accelerates the build-test-ship cycle from months to weeks. One developer, one AI partner, zero compromises on quality.

Relegate is the background-service sibling of [GideonMail](https://github.com/gbroeckling/gideonmail). Same engine, same features, no desktop — just quiet, reliable email management that starts on boot and never stops.

---

## License

MIT License — see [LICENSE](LICENSE).

Copyright (c) 2026 Garry Broeckling.
