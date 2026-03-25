# Relegate — Marketing Plan

## Positioning

**Tagline:** Put old email accounts on autopilot.

**One-liner:** Relegate is a background service that monitors neglected email accounts with AI triage, SMS alerts, and auto-cleanup — so you never miss what matters from accounts you stopped checking.

**Category:** Email management service / AI email automation

---

## Target Audience

### Primary
- **Small business owners** with old business emails from past ventures
- **Server admins** drowning in automated notifications from ISPConfig, cPanel, Plesk
- **Domain owners** with catch-all addresses collecting spam and occasional real mail
- **IT professionals** managing multiple legacy email accounts

### Secondary
- **Developers** who run their own mail servers
- **Privacy-conscious users** who run self-hosted email
- **Side project owners** with shared inboxes that occasionally get real customers

---

## Key Messages

1. **"You can't delete it. You won't check it. Relegate it."**
   - Everybody has at least one email account they ignore
   - Relegate makes ignoring it safe

2. **"AI reads your old email so you don't have to"**
   - Claude triages every incoming message
   - Texts you only when it matters

3. **"8 security filters for the inbox you forgot about"**
   - Neglected accounts are security risks
   - Relegate keeps them clean

4. **"Set it up once. It runs forever."**
   - Windows service — starts on boot
   - Standing instructions persist
   - No app to open

---

## Content Strategy

### Launch Content (Before June 1)
- [ ] Product announcement post on GitHub
- [ ] Reddit posts: r/selfhosted, r/sysadmin, r/email, r/homelab
- [ ] Hacker News Show HN post
- [ ] Dev.to article: "How I put 5 old email accounts on autopilot with AI"
- [ ] Blog post: "The email accounts you forgot are security risks"

### Launch Day (June 1)
- [ ] GitHub release with full documentation
- [ ] Product Hunt launch
- [ ] Twitter/X announcement thread
- [ ] Reddit launch posts

### Post-Launch
- [ ] Video demo: "Watch Relegate manage an email account in real time"
- [ ] Case study: "Server admin mailbox: from 500 daily emails to 3 texts per week"
- [ ] Comparison post: "Relegate vs email forwarding vs server-side rules"

---

## Channel Strategy

### GitHub (Primary)
- Well-documented README with clear use cases
- Issue templates for bugs and features
- Release notes with every update
- Cross-links to GideonMail for current testing

### Reddit
| Subreddit | Angle |
|-----------|-------|
| r/selfhosted | "Open-source AI email triage that runs as a service" |
| r/sysadmin | "Stop drowning in cron email — AI filters the noise" |
| r/homelab | "Background service for managing old IMAP accounts" |
| r/email | "Put neglected email accounts on autopilot" |
| r/node | "Electron-free Node.js email management service" |

### Hacker News
- Show HN: "Relegate — AI-powered background service for old email accounts"
- Focus on the technical architecture (Node.js service, 8 security filters, IMAP)

### Product Hunt
- Category: Productivity / Email
- Maker story: solo developer, AI-assisted development
- Demo GIF showing SMS alert from an old email account

---

## GitHub Topics

```
email, imap, smtp, ai-email, email-automation, email-security,
sms-notifications, windows-service, self-hosted, email-client,
email-triage, ai-assistant, claude, background-service
```

---

## Social Preview Image

Create 1280×640 image with:
- Relegate logo (target + arrow, adapted)
- "Put old email accounts on autopilot"
- Dark theme matching the product aesthetic
- "Beta: June 1, 2026"

---

## Pre-Launch Funnel

```
See Relegate README
    ↓
"Try features now in GideonMail"
    ↓
Install GideonMail → test AI, SMS, calendar
    ↓
Star Relegate repo for beta notification
    ↓
June 1: Relegate beta release
```

---

## Metrics to Track

- GitHub stars (Relegate + GideonMail)
- GideonMail installs (npm install count)
- Issue/discussion engagement
- Reddit/HN upvotes and comments
- Textbelt API key signups (indirect measure of active users)

---

## Competitive Landscape

| Competitor | Weakness Relegate exploits |
|-----------|---------------------------|
| Email forwarding | No AI, no filtering, no calendar |
| Server-side Sieve rules | No AI, no SMS, no calendar, hard to configure |
| SaneBox | $7/mo, cloud-dependent, no self-hosted |
| Clean Email | $10/mo, cloud-dependent, privacy concerns |
| Thunderbird filters | Needs app open, no AI, no SMS |

**Relegate's edge:** Open source, self-hosted, AI-powered, runs as a service, free (bring your own API keys).
