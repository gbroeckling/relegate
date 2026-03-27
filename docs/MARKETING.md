# Relegate — Marketing Plan

## Positioning

**Tagline:** Put old email accounts on autopilot.

**One-liner:** Relegate is a background service that monitors neglected email accounts with AI triage, SMS alerts, calendar integration, and full autopilot — so you never miss what matters from accounts you stopped checking.

**Category:** Email management service / AI email automation

**Status:** Beta release June 1, 2026. All features testable NOW in [GideonMail](https://github.com/gbroeckling/gideonmail).

---

## What Makes Relegate Different (2026 Feature Set)

The feature list has grown far beyond basic email filtering. Relegate is now a complete AI email operations platform:

### AI Intelligence Layer
- **Voice Learning** — AI samples your sent emails and learns your writing style. Every draft sounds like you wrote it.
- **Thread Summarization** — long email chains condensed to 1-2 sentences for SMS alerts
- **Commitment Tracking** — AI scans your outgoing emails for promises ("I'll send that by Friday"), tracks them, texts you before deadlines
- **Sender Reputation Learning** — tracks which senders you open, reply to, delete, or ignore. Suggests role changes over time.
- **Standing Instructions** — persistent rules the AI follows on every check ("always flag emails from my accountant", "delete anything from noreply addresses")

### Full Autopilot (Low Touch Mode — Experimental)
- **Auto-Categorize** — AI sorts every unknown email: spam, newsletter, receipt, notification, action, meeting, deadline
- **Auto-File** — moves to Newsletters/Receipts/Notifications folders automatically
- **Auto-Draft** — AI writes replies in your learned voice, sends to your phone for one-tap approval
- **Auto-Unsubscribe** — detects List-Unsubscribe headers on newsletters, unsubscribes via mailto or HTTP one-click
- **Auto-Nudge** — when your sent emails go unanswered for N days, auto-sends a polite follow-up in your voice
- **Auto-Schedule** — creates calendar events with AI-extracted date, time, location, and meeting links

### Smart Sender Management (People — 6 Roles)
| Role | What happens |
|------|-------------|
| **VIP** | Always texts you. Meetings auto-detected + auto-scheduled. Spam filters skipped. |
| **Watch** | AI analyzes every email. Configurable: SMS, auto-calendar, flag, auto-reply. |
| **Daily Update** | Batched into AI-summarized morning briefing. Green in inbox. No individual alerts. |
| **Blocked** | Dark red. Auto-deleted after 7 days. Always spam-filtered. |
| **Muted** | Grey. No notifications. Spam filters skipped. |
- Domain-wide rules (@domain.com)
- Inline role switching
- Add from any open email (sender or entire domain)

### Phone-Based Control (Action Email Relay)
- Branded HTML action emails with one-tap buttons (Accept, Decline, Reschedule, Reply, Later, Ignore)
- **Security-coded** — each action email has a unique 12-char hex verification token
- Replies without valid code are rejected and logged
- Processed action emails auto-delete from inbox
- Meeting action emails include full details: date, time, location, meeting link, reschedule from→to

### Calendar Intelligence
- **ICS attachment parsing** — reads calendar invites from VIP and Watch senders
- **Meeting link extraction** — Zoom, Teams, Meet, Webex URLs included in SMS and calendar events
- **AI constructs links from partial info** — "Zoom ID: 123 456 7890" becomes a full join URL
- **Reschedule detection** — same sender updates existing event instead of creating duplicates
- **Conflict detection** — checks calendar before scheduling
- **Permanent OAuth** with refresh tokens — stays connected

### Daily Intelligence
- **Smart Digest Email** — daily branded HTML email with AI summaries:
  - Needs Your Attention (red) — VIP/Watch emails
  - FYI — New & Unread (amber)
  - Auto-Handled by GideonMail (green)
  - Your Open Commitments (purple)
  - Sender Suggestions (cyan) — reputation-based role recommendations
- **Morning Briefing SMS** — unread count, VIP count, calendar, + Daily Update group summaries
- **Daily Update Groups** — batch senders like Amazon, UPS, PayPal into one daily digest instead of individual alerts

### Security (8 Filters)
SpamAssassin, Spamhaus ZEN, VirusTotal, Safe Browsing, PhishTank, AbuseIPDB, ClamAV, Bayesian learning. VIP/Watch/Muted/Daily immune from filtering.

---

## Target Audience

### Primary
- **Small business owners** with old business emails from past ventures
- **Server admins** drowning in automated notifications from ISPConfig, cPanel, Plesk
- **Domain owners** with catch-all addresses collecting spam and occasional real mail
- **IT professionals** managing multiple legacy email accounts

### Secondary
- **Developers** who run their own mail servers
- **Privacy-conscious users** who run self-hosted email (no cloud, no telemetry)
- **Side project owners** with shared inboxes that occasionally get real customers
- **Busy professionals** who want AI to handle routine email without changing providers

---

## Key Messages

1. **"You can't delete it. You won't check it. Relegate it."**
   - Everybody has at least one email account they ignore
   - Relegate makes ignoring it safe — and smart

2. **"AI reads your email, learns your voice, and handles it for you"**
   - Claude triages every incoming message
   - Drafts replies that sound like you
   - Tracks your commitments so nothing falls through the cracks

3. **"Your phone is your inbox"**
   - SMS alerts for what matters
   - Action emails with one-tap approve/decline/reply
   - Daily digest with AI summaries
   - You never need to open the app

4. **"8 security filters for the inbox you forgot about"**
   - Neglected accounts are security risks
   - Relegate keeps them clean and threat-free

5. **"Set it up once. It runs forever."**
   - Windows service — starts on boot, runs silently
   - Standing instructions persist
   - AI learns and improves over time

---

## Content Strategy

### Pre-Launch (Now through May 2026)

**GitHub:**
- [x] Comprehensive README with feature showcase
- [x] Full feature documentation
- [x] Architecture documentation
- [x] API setup guide
- [x] Troubleshooting guide
- [x] Marketing strategy (this document)
- [x] Issue templates
- [x] Security policy
- [ ] Social preview image (1280×640)
- [ ] Demo screenshots/GIFs

**Content pieces to write:**
- [ ] Dev.to: "How I built an AI email autopilot that learns my voice"
- [ ] Dev.to: "I put 5 old email accounts on autopilot — here's what happened"
- [ ] Blog: "The email accounts you forgot are security risks"
- [ ] Blog: "Why I built a commitment tracker into my email client"
- [ ] Blog: "From 500 daily emails to 3 texts per week: a server admin's story"

**Reddit warm-up (before beta):**
- [ ] r/selfhosted — "Show off: AI email triage for my ISPConfig server"
- [ ] r/sysadmin — "Built a service to filter cron email with AI — open source"
- [ ] r/homelab — "Background service that manages old IMAP accounts with AI"
- [ ] r/email — "Put neglected email accounts on autopilot"

### Launch Week (June 1, 2026)

**Day 1:**
- [ ] GitHub release v0.1.0-beta with full documentation
- [ ] Product Hunt launch
- [ ] Hacker News: Show HN post
- [ ] Reddit launch posts (all target subreddits)
- [ ] Twitter/X announcement thread

**Day 2-3:**
- [ ] Respond to all comments/questions
- [ ] Cross-post to r/node, r/javascript, r/opensource
- [ ] LinkedIn article

**Day 4-7:**
- [ ] Follow up on Product Hunt comments
- [ ] First issue triage and responses
- [ ] Dev.to launch article

### Post-Launch
- [ ] Video demo: "Watch Relegate manage an email account in real time"
- [ ] Case study: server admin mailbox scenario
- [ ] Comparison article: "Relegate vs SaneBox vs email forwarding"
- [ ] Feature spotlight posts (commitment tracking, voice learning, smart digest)
- [ ] User testimonials (if beta testers provide feedback)

---

## Channel Strategy

### GitHub (Primary)
- Professional README with clear problem/solution narrative
- Comprehensive docs/ directory
- Issue templates for bugs and features
- Release notes with every update
- Cross-links to GideonMail for immediate testing
- Topics: email, imap, ai-email, email-automation, sms-notifications, windows-service, self-hosted, ai-assistant, claude, background-service

### Reddit
| Subreddit | Angle | Key Feature to Highlight |
|-----------|-------|------------------------|
| r/selfhosted | "Open-source AI email triage that runs as a service" | No cloud, local-only, self-hosted |
| r/sysadmin | "Stop drowning in cron email — AI filters the noise" | Smart categorization, SMS for real alerts |
| r/homelab | "Background service for managing old IMAP accounts" | Windows service, set-and-forget |
| r/email | "AI autopilot for neglected email accounts" | Voice learning, auto-draft, auto-unsubscribe |
| r/node | "Built a complete email AI platform in Node.js" | Technical architecture, Claude integration |
| r/javascript | "Electron → Windows service: AI email management" | Engine extraction story |
| r/opensource | "MIT-licensed AI email manager with 8 security filters" | Open source, privacy-first |
| r/artificial | "Using Claude to manage email — voice learning + commitment tracking" | AI capabilities showcase |

### Hacker News
- Show HN: "Relegate — AI background service that manages old email accounts"
- Technical focus: Node.js, IMAP, 8 security filters, Claude API integration
- Emphasize: open source, self-hosted, no telemetry, no cloud

### Product Hunt
- Category: Productivity / Email / AI Tools
- Maker story: solo developer + Claude, dog-fooded on own ISPConfig server
- Hero feature: "Your phone becomes your inbox" (action emails + SMS)
- Demo: screenshot of Smart Digest email + SMS alert

### Dev.to
- Technical deep dives on interesting features
- "Building with Claude" series about AI-assisted development
- Architecture posts about the engine extraction from Electron to service

---

## Social Preview Image

Create 1280×640 image with:
- Relegate logo (target + arrow icon)
- "Put old email accounts on autopilot"
- Dark theme (#111113 background, #7c6cff accent)
- Feature highlights: AI Triage • SMS Alerts • Calendar • Autopilot
- "Beta: June 1, 2026"
- "Try it now → GideonMail"

---

## Pre-Launch Funnel

```
See Relegate README / Reddit post / HN
    ↓
"All features available now in GideonMail"
    ↓
Clone GideonMail → npm install → npm start
    ↓
Test: AI triage, SMS alerts, calendar, Low Touch autopilot
    ↓
Star Relegate repo → Watch for beta notification
    ↓
June 1: Relegate beta release (background service)
```

---

## Metrics to Track

| Metric | Source | Target (month 1) |
|--------|--------|------------------|
| GitHub stars (Relegate) | GitHub | 100+ |
| GitHub stars (GideonMail) | GitHub | 200+ |
| GideonMail clones | git traffic | 50+ |
| Issues opened | GitHub | 20+ (means engagement) |
| Reddit upvotes | Reddit | 50+ per post |
| HN points | HN | 50+ |
| Product Hunt upvotes | PH | 100+ |
| Textbelt signups | Indirect | 10+ active users |

---

## Competitive Landscape

| Competitor | Price | Weakness Relegate exploits |
|-----------|-------|---------------------------|
| **Email forwarding** | Free | No AI, no filtering, no calendar, no smart alerts |
| **Server-side Sieve** | Free | No AI, no SMS, no calendar, hard to configure, no learning |
| **SaneBox** | $7/mo | Cloud-dependent, no self-hosted, no SMS, no calendar, no voice learning |
| **Clean Email** | $10/mo | Cloud-dependent, privacy concerns, no SMS, no action emails |
| **Thunderbird filters** | Free | Needs app open, no AI, no SMS, no calendar, no autopilot |
| **Gmail filters** | Free | Google lock-in, no AI triage, no SMS, no commitment tracking |
| **Hey.com** | $99/yr | Expensive, cloud-only, no self-hosted, limited automation |

**Relegate's edge:** Open source. Self-hosted. AI-powered. Learns your voice. Tracks your commitments. Runs as a service. Free (bring your own API keys). Privacy-first — no telemetry, no cloud sync, everything local.

---

## Feature Comparison for Marketing

| Feature | Relegate | SaneBox | Clean Email | Gmail | Thunderbird |
|---------|:-------:|:-------:|:-----------:|:-----:|:-----------:|
| AI email triage | ✅ | ❌ | ❌ | ❌ | ❌ |
| Learns your voice | ✅ | ❌ | ❌ | ❌ | ❌ |
| Auto-draft replies | ✅ | ❌ | ❌ | ✅* | ❌ |
| Commitment tracking | ✅ | ❌ | ❌ | ❌ | ❌ |
| SMS alerts | ✅ | ❌ | ❌ | ❌ | ❌ |
| Action emails (phone control) | ✅ | ❌ | ❌ | ❌ | ❌ |
| Meeting link extraction | ✅ | ❌ | ❌ | ✅ | ❌ |
| Calendar auto-create | ✅ | ❌ | ❌ | ✅ | ❌ |
| Reschedule detection | ✅ | ❌ | ❌ | ❌ | ❌ |
| Auto-unsubscribe | ✅ | ✅ | ✅ | ✅ | ❌ |
| 8 security filters | ✅ | ❌ | ❌ | Partial | ❌ |
| Runs without UI | ✅ | N/A | N/A | N/A | ❌ |
| Self-hosted | ✅ | ❌ | ❌ | ❌ | ✅ |
| Open source | ✅ | ❌ | ❌ | ❌ | ✅ |
| Free | ✅ | ❌ | ❌ | ✅ | ✅ |

*Gmail Smart Reply is limited and cloud-only

---

## Announcement Draft (for June 1)

**Title:** "Relegate: Put old email accounts on autopilot — AI triage, SMS alerts, calendar integration, and full autopilot mode"

**Body:**
> I built Relegate because I have 5 email accounts I never check but can't delete. My ISPConfig server gets 200 emails a day — 3 of them matter. My old business email still gets client inquiries. My domain catch-all is 99% spam but my bank uses it.
>
> Relegate connects to any IMAP account and becomes its full-time manager:
> - AI reads every email and decides: important, routine, or junk
> - Texts you when something actually needs your attention
> - Learns your writing style and drafts replies that sound like you
> - Tracks promises you make in emails and nudges you before deadlines
> - Auto-creates calendar events with meeting links
> - Sends you a daily digest email with AI summaries
> - 8 security filters protect neglected inboxes
>
> Runs as a Windows service. Starts on boot. No window. No tray icon. Just quiet, reliable email management in the background.
>
> **All features are testable RIGHT NOW** in GideonMail, the desktop version: `git clone https://github.com/gbroeckling/gideonmail && npm install && npm start`
>
> Open source. MIT licensed. Self-hosted. No telemetry. No cloud.
>
> GitHub: github.com/gbroeckling/relegate

---

Built by **Garry Broeckling**. AI-assisted with **Claude** by Anthropic — all architecture, product decisions, and testing are human-directed.
