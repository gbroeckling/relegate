# Relegate Features

> **All features listed here are available today in [GideonMail](https://github.com/gbroeckling/gideonmail).** Relegate will run the same engine as a background service without a desktop UI.

## AI Email Triage

Powered by Claude (Anthropic), the AI engine reads every incoming email and decides what action to take:

- **Urgency scoring** — URGENT, normal, or skip
- **Smart summaries** — one-line descriptions for SMS alerts
- **Meeting detection** — identifies emails about scheduled events
- **Standing instructions** — persistent rules you teach once (e.g., "always flag emails from my accountant", "delete anything from noreply addresses")
- **Per-sender analysis** — Watch list senders get full AI analysis on every email

**Cost:** ~$0.003 per email analyzed. $5 of Anthropic credit lasts months.

## Smart Sender Management

One unified People list with four roles:

| Role | SMS | Spam Filter | Auto-delete | Calendar |
|------|-----|-------------|-------------|----------|
| **VIP** | Always | Skipped | No | Meeting detection |
| **Watch** | Configurable | Skipped | No | Auto-create events |
| **Blocked** | Never | Always | After 7 days | No |
| **Muted** | Never | Skipped | No | No |

## SMS Notifications

Text messages when it matters — via Textbelt ($10 for 1,000 texts):

- VIP sender alerts
- AI urgency detection
- Meeting detection: "MEETING from Nicole: Dinner Friday 7pm"
- Conversation alerts: threads you've replied to 2+ times in 6 months
- Quiet hours (10pm–7am), rate limits, batch mode
- Catches up on emails from while the service was stopped

## Google Calendar Integration

- Auto-creates events from Watch list senders
- Meeting detection for VIP emails
- Permanent OAuth — stays connected via refresh tokens
- No attendees invited unless explicitly approved

## Security Filters

8 scanning layers for emails from unknown and blocked senders:

1. **SpamAssassin Headers** — reads server-side scores (free)
2. **Spamhaus ZEN** — DNS blocklist (free)
3. **VirusTotal** — URL scanning, 70+ engines (free tier: 500/day)
4. **Google Safe Browsing** — URL threats (free tier: 10k/day)
5. **PhishTank** — phishing URLs (free)
6. **AbuseIPDB** — IP reputation (free tier: 1k/day)
7. **ClamAV** — local antivirus (free)
8. **Bayesian Filter** — learns from patterns over time

VIP, Watch, and Muted senders are immune from spam filters.

## Auto-Cleanup

- Blocked sender emails auto-deleted after 7 days
- Conversation tracking with configurable lookback
- Persistent SMS dedup — never sends the same alert twice

## Configuration

All settings stored locally in JSON. Compatible with GideonMail — migrate by copying the config file.

Planned web dashboard on localhost for browser-based configuration.
