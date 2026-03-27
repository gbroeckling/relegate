# Relegate — Complete Feature Reference

> **Every feature on this page is production-ready today.** The engine that powers Relegate ships in [GideonMail](https://github.com/gbroeckling/gideonmail). Relegate packages the same engine as a silent Windows background service — no desktop UI, no browser tab, no tray icon. It just runs.

---

## Table of Contents

1. [AI Email Triage (Claude-Powered)](#1-ai-email-triage-claude-powered)
2. [Low Touch Autopilot (Experimental)](#2-low-touch-autopilot-experimental)
3. [Smart Sender Management (People)](#3-smart-sender-management-people)
4. [SMS Notifications (Textbelt)](#4-sms-notifications-textbelt)
5. [Action Email Relay](#5-action-email-relay)
6. [Google Calendar Integration](#6-google-calendar-integration)
7. [Smart Digest Email](#7-smart-digest-email)
8. [Sender Reputation Learning](#8-sender-reputation-learning)
9. [Commitment Tracking](#9-commitment-tracking)
10. [Daily Update Groups](#10-daily-update-groups)
11. [Security Filters (8 Layers)](#11-security-filters-8-layers)
12. [Auto-Cleanup](#12-auto-cleanup)
13. [Configuration](#13-configuration)

---

## 1. AI Email Triage (Claude-Powered)

Every incoming email passes through Anthropic's Claude before it reaches you. The AI reads the full message — subject, body, headers, attachments — and makes a series of decisions in real time so you never have to.

### Urgency Scoring

Each email is assigned a priority level: **URGENT**, **normal**, or **skip**. Urgent emails trigger immediate SMS alerts. Normal emails appear in the daily digest. Skipped emails (marketing blasts, social notifications, automated receipts) are filed or ignored silently. The AI considers sender history, language cues, deadlines, and your standing instructions to make the call.

**How it works:** Claude analyzes the email content, sender context, and your configured rules in a single pass. The urgency score determines every downstream action — whether you get a text, whether the email shows up in your digest, and whether an action email is generated.

**Why it matters:** You stop checking email "just in case." Urgent messages find you. Everything else waits until you are ready.

### Smart Summaries

Every email is distilled into a one-line summary suitable for an SMS or a digest row. These are not truncated subject lines — the AI reads the full email and writes a fresh summary that captures the actual point.

**How it works:** Claude generates a concise natural-language summary from the full email body, not just the subject. Summaries are used in SMS alerts, action emails, and the daily digest.

**Why it matters:** You get the substance of a 12-paragraph email in a single sentence on your phone lock screen.

### Meeting Detection

The AI identifies emails about scheduled events by reading the email body, not just the subject line. "Let's grab lunch Thursday at noon" is detected just as reliably as a formal calendar invite.

**How it works:** Claude scans for temporal references, location mentions, and scheduling language. Detected meetings are flagged for calendar creation and SMS alerts include meeting details and join links.

**Why it matters:** You never miss a meeting buried in a casual email thread.

### Voice Learning

Relegate reads your sent emails and drafts to learn how you write — your tone, your phrasing, your sign-offs, your level of formality with different people. When it drafts a reply, it sounds like you wrote it.

**How it works:** The AI samples your outgoing messages to build a writing profile. This profile is used whenever auto-draft or auto-nudge generates a reply. The result reads like something you would actually send, not a generic AI template.

**Why it matters:** People on the other end never know the difference. Your replies maintain your relationships and your reputation.

### Thread Summarization

Long email chains — the ones with 15 RE: prefixes and three different subconversations — are condensed into a 1-2 sentence summary. This summary is included in SMS alerts and action emails so you have full context without scrolling.

**How it works:** Claude processes the entire thread, identifies the key points and latest developments, and produces a condensed summary that captures the current state of the conversation.

**Why it matters:** You can make a decision about a 30-message thread from a single SMS.

### Standing Instructions

Persistent rules you teach once and never repeat. "Always flag emails from my accountant." "Delete anything from noreply addresses." "Treat invoices over $500 as urgent." These instructions persist across sessions and apply to every email.

**How it works:** Standing instructions are stored in your local config and injected into every AI analysis pass. They override default behavior and stack with sender roles.

**Why it matters:** You train the system once. It remembers forever.

### Per-Sender AI Analysis

Senders on your Watch list receive full AI analysis on every email — not just urgency scoring, but detailed content breakdown, action item extraction, and contextual notes.

**How it works:** Watch list emails get an enhanced AI pass that goes beyond triage. The full analysis is included in SMS alerts, action emails, and the daily digest.

**Why it matters:** For the handful of people who matter most to your work, you get AI-powered briefings on every message.

### Cost

**~$0.003 per email analyzed.** Five dollars of Anthropic API credit processes roughly 1,600 emails. For most neglected accounts, that is months of coverage.

---

## 2. Low Touch Autopilot (Experimental)

Autopilot is fully autonomous email processing. Once configured, it handles your inbox without any interaction from you — categorizing, filing, replying, unsubscribing, following up, and scheduling. You approve drafts from your phone with a single tap. Everything else happens silently.

> **EXPERIMENTAL** — Autopilot features are functional and shipping but are marked experimental while edge cases are refined. All autonomous actions are logged and reversible.

### Auto-Categorize

Every incoming email is classified by the AI into one of seven categories:

| Category | What it means |
|----------|---------------|
| **spam** | Junk, phishing attempts, unsolicited marketing |
| **newsletter** | Subscribed content, digests, blog updates |
| **receipt** | Purchase confirmations, invoices, payment notifications |
| **notification** | Automated alerts from apps and services |
| **action** | Emails that require a human response |
| **meeting** | Scheduling requests, calendar invites, time-sensitive coordination |
| **deadline** | Emails containing due dates, expiration warnings, time-bound requests |

**How it works:** Claude reads the full email and assigns a single category. The category drives downstream automation — filing, drafting, scheduling, or ignoring.

**Why it matters:** Your inbox stops being a single undifferentiated pile. Every email has a purpose and a destination.

### Auto-File

Categorized emails are moved to dedicated IMAP folders automatically:

- **Newsletters** folder for newsletters
- **Receipts** folder for receipts and invoices
- **Notifications** folder for automated notifications

**How it works:** After categorization, emails matching file-able categories are moved server-side via IMAP. The folders are created automatically if they do not exist.

**Why it matters:** Your inbox contains only emails that need your attention. Everything else is organized and findable.

### Auto-Draft Replies

When the AI identifies an email that needs a response, it writes a draft in your learned voice and sends it to you as an action email for one-tap approval.

**How it works:** Claude uses your voice profile to compose a contextually appropriate reply. The draft is embedded in a branded action email sent to your inbox with "Send This Reply" and "Edit" buttons. Thread context is summarized and included so you can approve confidently.

**Why it matters:** You review and send replies from your phone lock screen in seconds. The AI does the writing; you keep the control.

### Auto-Unsubscribe

Detected newsletters with List-Unsubscribe headers are automatically unsubscribed. Relegate supports both methods defined in RFC 8058:

- **mailto:** — sends the unsubscribe email on your behalf
- **HTTP one-click** — posts to the unsubscribe URL directly

**How it works:** The AI identifies newsletters, checks for List-Unsubscribe and List-Unsubscribe-Post headers, and executes the appropriate unsubscribe mechanism. No manual clicking required.

**Why it matters:** The newsletters you never read stop coming. Automatically. Every day your inbox gets a little quieter.

### Auto-Nudge Follow-Ups

When you send an email and the recipient does not respond within a configurable number of days, Relegate sends a polite follow-up in your voice.

**How it works:** Outgoing emails are tracked. After N days without a reply, the AI generates a natural follow-up ("Just wanted to make sure this didn't get buried...") using your voice profile and sends it automatically.

**Why it matters:** You never have to remember to follow up. Important threads do not die because someone forgot to reply.

### Auto-Schedule Calendar Events

Emails containing meeting information are automatically converted into Google Calendar events with AI-extracted date, time, and location.

**How it works:** This is the same calendar integration described in Section 6, triggered automatically by Autopilot instead of requiring manual confirmation. The AI extracts scheduling details from the email body and creates the event.

**Why it matters:** Meetings appear on your calendar the moment they are proposed. No manual entry, no missed appointments.

---

## 3. Smart Sender Management (People)

Every sender and domain in Relegate has a role. The role determines exactly what happens when their email arrives — whether you get a text, whether spam filters run, whether replies are auto-drafted, and whether meetings are auto-scheduled. One unified People list. Six roles. Complete control.

### The Roles

| Role | SMS Alerts | Spam Filter | Auto-Delete | Calendar | Special Behavior |
|------|-----------|-------------|-------------|----------|-----------------|
| **VIP** | Always | Skipped | Never | Meeting detection + auto-schedule | Texts you immediately with AI summary. Meetings are auto-detected and scheduled. Spam filters never touch their email. |
| **Watch** | Configurable | Skipped | Never | Auto-create events | Full AI analysis on every email. Configurable SMS and calendar actions. |
| **Daily Update** | Never (batched) | Skipped | Never | No | Batched into a morning briefing. Green highlighting in inbox. No individual alerts. |
| **Blocked** | Never | Always | After 7 days | No | Email is filtered, quarantined, and auto-deleted after 7 days. |
| **Muted** | Never | Skipped | Never | No | Email arrives silently. No notifications, no analysis, no spam filtering. |
| *(Unassigned)* | AI decides | Full scan | Never | No | Default behavior. AI triage determines urgency and actions. |

### Domain-Wide Rules

Assign a role to an entire domain (`@company.com`) and every sender from that domain inherits the role. Individual sender overrides still take priority.

**How it works:** Domain rules are checked after individual sender rules. If no individual rule exists, the domain rule applies. This is ideal for companies where every employee should be treated the same way.

**Why it matters:** One rule covers an entire organization. You do not need to add 50 people from the same company individually.

### Inline Role Switching

Change a sender's role from any open email — no navigating to a settings page. See an email from someone who should be VIP? Switch them right there.

**How it works:** The sender management interface is accessible inline. Role changes take effect immediately on the next email from that sender.

**Why it matters:** Managing senders is a zero-friction, one-second action.

### Add From Any Open Email

Any email you are viewing can be used to add the sender to your People list. No copying addresses, no switching screens.

**How it works:** The sender's address is extracted from the email headers and presented for role assignment.

**Why it matters:** Building your People list happens naturally as you encounter senders, not as a separate configuration chore.

---

## 4. SMS Notifications (Textbelt)

Relegate texts you when it matters and stays silent when it does not. Notifications are powered by Textbelt — a simple, reliable SMS API with no subscriptions, no contracts, and no monthly fees.

### VIP Alerts with AI Summaries

When a VIP sender emails you, you get an immediate text with the AI-generated summary. Not the subject line — the actual point of the email, in one sentence.

**How it works:** VIP emails trigger an SMS containing the sender name, AI summary, and any relevant details (meeting times, action items). The message is composed to be useful on a phone lock screen without opening anything.

**Why it matters:** The most important emails in your inbox reach you in seconds, wherever you are.

### Meeting Detection with Join Links

Meeting-related emails include the meeting details and a clickable join link directly in the SMS. Zoom, Microsoft Teams, Google Meet, and Webex links are detected and included.

**How it works:** The AI identifies meeting emails, extracts the online meeting URL, and appends it to the SMS. If only a partial meeting ID is provided (e.g., "Zoom ID: 123 456 7890"), the AI constructs the full join URL.

**Why it matters:** You tap the link in your text message and you are in the meeting. No searching through email.

### Conversation Alerts

Threads you have been actively participating in (2+ replies in the last 6 months) trigger SMS alerts when new replies arrive, even if the sender is not VIP.

**How it works:** Relegate tracks your reply history per thread. Active conversations are flagged for SMS notification regardless of sender role.

**Why it matters:** Ongoing conversations stay on your radar without promoting every participant to VIP.

### Quiet Hours, Rate Limits, and Batch Mode

- **Quiet hours** — no texts between configurable hours (default 10 PM to 7 AM). Queued messages are delivered when quiet hours end.
- **Rate limits** — prevents SMS floods from a burst of incoming email.
- **Batch mode** — groups multiple alerts into a single summary text instead of sending one per email.

**How it works:** All three controls operate on the SMS output queue. Emails are still processed in real time; only the notification delivery is throttled.

**Why it matters:** Your phone does not buzz at 2 AM, and a mailing list incident does not drain your SMS balance.

### History Lookback on Startup

When Relegate starts (or restarts after downtime), it scans recent emails for anything that should have triggered an alert while it was offline.

**How it works:** On startup, Relegate checks the inbox for unprocessed emails within a configurable lookback window and runs them through the normal triage pipeline. Alerts are sent for anything that qualifies.

**Why it matters:** A service restart does not create a blind spot. You are always covered.

### Cost

**$10 for 1,000 text messages** via Textbelt. No subscription. No expiration. At typical alert volumes, $10 lasts most users six months or more.

---

## 5. Action Email Relay

Action emails are branded HTML messages sent to your inbox with one-tap buttons that let you control your email from your phone — approve a reply, decline a meeting, reschedule, or dismiss — without ever opening the original email or launching an app.

### Branded HTML with One-Tap Buttons

Action emails arrive as polished, mobile-optimized HTML with clearly labeled buttons: **Send This Reply**, **Approve**, **Decline**, **Reschedule**, **Later**, **Ignore**. The AI summary and any draft reply are embedded directly in the email.

**How it works:** When an email requires your input (a reply draft, a meeting request, a flagged message), Relegate generates an action email and delivers it to your inbox. Each button maps to a specific backend action.

**Why it matters:** Your inbox becomes a control panel. You make decisions with single taps instead of composing responses.

### Security-Coded Verification

Every action email contains a unique 12-character hexadecimal verification token. Replies and button presses are validated against this token. Forged or replayed action emails are rejected.

**How it works:** A cryptographically random token is generated for each action email and stored locally. Incoming responses are matched against the stored token before any action is executed.

**Why it matters:** Nobody can trigger actions on your behalf by spoofing an action email. Every tap is verified.

### Reschedule Button for Meetings

Meeting-related action emails include a **Reschedule** button that lets you propose a new time directly from the action email.

**How it works:** Tapping Reschedule triggers a follow-up flow that updates the calendar event and optionally sends a reschedule message to the organizer.

**Why it matters:** Rescheduling a meeting takes one tap instead of a chain of back-and-forth emails.

### Auto-Delete Processed Action Emails

After you act on an action email (or after the underlying email is handled), the action email is automatically removed from your inbox. Deletion is verified by matching the security code.

**How it works:** Once a response with a valid token is processed, Relegate deletes the corresponding action email via IMAP. The security code ensures only the correct action email is removed.

**Why it matters:** Action emails are transient by design. They appear when needed and disappear when done. Your inbox stays clean.

### Phone-Based Inbox Control

The entire action email system is designed for phone use. No app to install. No browser to open. Everything happens inside your existing email client.

**Why it matters:** You manage a neglected email account from your phone's notification shade and default mail app. Zero additional software.

---

## 6. Google Calendar Integration

Relegate reads your email and puts meetings on your calendar — with the right date, time, location, and join link — so you do not have to.

### AI Date/Time/Location Extraction

The AI reads the full email body and extracts scheduling details: date, time, duration, location, and any special notes. This works on formal invitations and casual messages alike.

**How it works:** Claude parses natural language scheduling references ("next Tuesday at 3," "the 15th at noon EST," "same time as last week") and converts them into structured calendar event data.

**Why it matters:** You do not need a formal calendar invite for a meeting to appear on your calendar. "Let's meet Thursday" is enough.

### ICS Attachment Parsing

Standard calendar attachments (text/calendar MIME parts and .ics files) are parsed automatically. VEVENT, DTSTART, DTEND, LOCATION, and other iCalendar fields are extracted and used to create precise calendar events.

**How it works:** Relegate detects text/calendar content types and .ics attachments, parses the iCalendar data, and feeds it to the AI alongside the email body for accurate event creation.

**Why it matters:** Formal calendar invites are handled perfectly. The ICS data ensures exact times and time zones.

### Online Meeting Link Extraction

Join URLs for Zoom, Microsoft Teams, Google Meet, and Webex are detected in the email body and added to the calendar event's description and location fields.

**How it works:** The AI scans for known meeting URL patterns. When only a partial meeting ID is provided (e.g., "Zoom Meeting ID: 123 456 7890, Passcode: abc"), the AI constructs the full join URL with embedded passcode.

**Why it matters:** You tap the meeting link in your calendar event and join. No hunting through email threads for the URL.

### Reschedule Detection

When the same sender sends an updated meeting time, Relegate updates the existing calendar event instead of creating a duplicate.

**How it works:** Events are matched by sender and meeting subject. When a reschedule is detected, the existing event's time, location, and details are updated in place.

**Why it matters:** Your calendar stays clean. One meeting, one event — even if the time changes three times.

### Conflict Detection

Before creating a calendar event, Relegate checks your existing schedule for conflicts and flags them.

**How it works:** The Google Calendar API is queried for overlapping events in the proposed time window. Conflicts are reported in the action email or SMS alert.

**Why it matters:** You know about double-bookings before they happen, not when you show up to the wrong meeting.

### Permanent OAuth with Refresh Tokens

Calendar access uses Google's OAuth 2.0 flow with persistent refresh tokens. You authenticate once and stay connected indefinitely.

**How it works:** The initial OAuth flow stores a refresh token locally. Relegate uses this token to obtain fresh access tokens automatically, without re-authentication.

**Why it matters:** Set it up once. It works until you revoke access. No re-login prompts, no expired sessions.

### No Attendees Invited Unless Approved

Calendar events are created on your calendar only. Other attendees are never invited or notified unless you explicitly approve the invitation.

**How it works:** Events are created with no attendee list by default. If attendee invitations are appropriate, they are staged for approval via action email.

**Why it matters:** Creating a calendar event does not accidentally send invitations to people who have already been invited by someone else.

---

## 7. Smart Digest Email

Once a day, Relegate sends you a single branded HTML email that summarizes everything that happened in your inbox. It is your morning briefing — organized, color-coded, and actionable.

### Daily Branded HTML Summary

The digest is a polished, mobile-friendly HTML email with your inbox activity organized into clear sections. It arrives at a configurable hour (default: morning).

**How it works:** Relegate aggregates all processed emails from the previous period, applies AI summarization, and renders the digest using a branded HTML template.

**Why it matters:** One email replaces the need to open your inbox at all. You read the digest, take any needed actions, and move on.

### Color-Coded Sections

| Section | Color | Contents |
|---------|-------|----------|
| **Needs Attention** | Red | Emails that require your response or decision |
| **FYI** | Amber | Important information that does not require action |
| **Auto-Handled** | Green | Emails that Autopilot processed without your input |
| **Commitments** | Purple | Promises you made in outgoing emails, with due dates |
| **Sender Suggestions** | Cyan | AI recommendations for sender role changes based on your behavior |

**How it works:** Each processed email is categorized into a digest section based on its triage result and any actions taken. AI summaries are included for every entry.

**Why it matters:** You can scan the red section in 30 seconds and know if anything needs your attention. Everything else is informational.

### Configurable Send Hour

Set the digest to arrive when you want it — first thing in the morning, during lunch, or end of day.

**How it works:** A configurable hour (24-hour format) controls when the digest is compiled and sent.

**Why it matters:** The digest fits your routine, not the other way around.

---

## 8. Sender Reputation Learning

Relegate watches how you interact with email from every sender and builds a behavioral profile over time. When the pattern is clear, it suggests role changes to automate what you are already doing manually.

### Interaction Tracking

Every email interaction is recorded per sender:

- **Opens** — you read the email
- **Replies** — you responded
- **Deletes** — you deleted without reading or shortly after opening
- **Ignores** — the email sat unread and unactioned

**How it works:** IMAP flag changes and sent-folder activity are monitored to build a per-sender interaction history. The data is stored locally and never leaves your machine.

**Why it matters:** Relegate learns who matters and who does not, based on your actual behavior — not your intentions.

### AI-Powered Role Suggestions

When interaction patterns reach clear thresholds, Relegate suggests role changes:

| Pattern | Suggestion |
|---------|-----------|
| Deleted **>70%** of their emails | Move to **Blocked** |
| Replied to **>50%** of their emails | Move to **Watch** |
| Ignored **>80%** of their emails | Move to **Muted** |

**How it works:** Sender statistics are evaluated periodically. Suggestions that meet the threshold are included in the Sender Suggestions section of the daily digest.

**Why it matters:** Your People list optimizes itself. Senders you consistently ignore get muted. Senders you consistently engage with get promoted. The system gets smarter every week.

### Surfaced in Smart Digest

Role suggestions appear in the daily digest with the sender name, current role, suggested role, and the behavioral data behind the recommendation. You approve or dismiss with a single action.

**Why it matters:** You stay in control. The AI recommends; you decide.

---

## 9. Commitment Tracking

Relegate reads your outgoing emails and identifies promises you have made — deadlines, deliverables, follow-ups. It tracks them, reminds you, and surfaces them in your daily digest so nothing falls through the cracks.

### AI Promise Detection

When you send an email containing a commitment ("I'll send the report by Friday," "Let me get back to you on that," "I'll have the numbers by EOD"), the AI extracts it and stores it.

**How it works:** Claude scans outgoing emails for language patterns indicating promises, obligations, or follow-up commitments. Detected commitments are stored with the recipient, the promise text, and any associated due date.

**Why it matters:** You make promises throughout the day without thinking about them. Relegate remembers every one.

### Due Date Extraction and Storage

Commitments with explicit deadlines are stored with their due date. Undated commitments are assigned a default 3-day follow-up window.

**How it works:** The AI extracts date references from commitment language and converts them to calendar dates. If no date is mentioned, a 3-day default is applied.

**Why it matters:** Every commitment has a deadline — explicit or implied. Nothing lingers indefinitely.

### SMS Nudges When Due or Overdue

When a commitment reaches its due date (or passes it), Relegate texts you a reminder with the recipient's name and the promise you made.

**How it works:** Commitment due dates are checked on each processing cycle. Due and overdue commitments trigger SMS alerts with the commitment details.

**Why it matters:** You find out about a forgotten promise before the other person has to remind you.

### Smart Digest Integration

All active commitments appear in the purple **Commitments** section of your daily digest, sorted by due date. Overdue items are flagged.

**Why it matters:** Your daily briefing includes a complete list of outstanding promises. One glance tells you what you owe and to whom.

---

## 10. Daily Update Groups

Some senders are important enough to track but not important enough to interrupt you. Daily Update groups batch these senders into a single morning briefing with AI-generated summaries. No individual alerts. No inbox clutter. Just a clean summary.

### Batch Senders and Domains

Assign any sender or domain to the Daily Update role. All their emails are collected and delivered as a single batched briefing.

**How it works:** Emails from Daily Update senders are processed and stored but do not trigger individual SMS alerts or action emails. They are aggregated into the morning briefing.

**Why it matters:** Shipping updates, invoice notifications, service alerts — important to know about, not important enough to interrupt your day.

### AI-Summarized Briefing

The morning briefing includes AI summaries for every Daily Update email, organized by sender. Deliveries, invoices, shipping updates, and routine notifications are condensed into scannable one-liners.

**How it works:** Claude summarizes each email and groups them by sender in the briefing. The briefing is delivered as part of the daily digest or as a standalone summary.

**Why it matters:** "3 packages shipped, 2 invoices received, AWS bill is $47.23" — in one paragraph instead of six separate emails.

### No Individual SMS Alerts

Daily Update senders never trigger individual text messages, regardless of urgency scoring. All communication is batched.

**Why it matters:** Your phone stays quiet. The information is there when you want it, not when it arrives.

### Spam Filters Skipped

Daily Update senders are exempt from spam filtering, just like VIP and Watch senders. Their email always arrives.

**Why it matters:** Automated notifications from services you care about are never accidentally flagged as spam.

### Green Highlighting in Inbox

Emails from Daily Update senders are visually distinguished with green highlighting in inbox views and digest sections.

**Why it matters:** You can instantly identify batched senders and know those emails are informational, not action-required.

---

## 11. Security Filters (8 Layers)

Emails from unknown and Blocked senders pass through eight independent scanning layers before they reach your inbox. Each layer catches a different class of threat. Together, they form a defense-in-depth system that stops spam, phishing, malware, and fraud.

### The Layers

| # | Layer | What It Catches | Cost |
|---|-------|----------------|------|
| 1 | **SpamAssassin Headers** | Server-side spam scores and flags | Free |
| 2 | **Spamhaus ZEN** | Known spam IPs and domains via DNS blocklist | Free |
| 3 | **VirusTotal** | Malicious URLs scanned against 70+ antivirus engines | Free tier: 500 lookups/day |
| 4 | **Google Safe Browsing** | Phishing, malware, and unwanted software URLs | Free tier: 10,000 lookups/day |
| 5 | **PhishTank** | Community-verified phishing URLs | Free |
| 6 | **AbuseIPDB** | IP addresses reported for abuse, scanning, or attacks | Free tier: 1,000 lookups/day |
| 7 | **ClamAV** | Virus and malware scanning of attachments (local engine) | Free |
| 8 | **Bayesian Filter** | Pattern-based spam detection that learns over time | Free |

### Immunity by Role

VIP, Watch, Muted, and Daily Update senders are **immune** from all spam and security filters. Their email is always delivered. Only emails from unknown and Blocked senders are scanned.

**How it works:** Sender role is checked before the security pipeline runs. Known senders with trusted roles bypass all eight layers.

**Why it matters:** People you trust are never delayed or filtered. People you do not know are thoroughly scanned. Blocked senders are scanned and quarantined.

---

## 12. Auto-Cleanup

Relegate keeps your inbox clean without manual intervention. Temporary emails are removed, blocked senders are purged, and duplicate alerts are prevented automatically.

### Blocked Sender Auto-Delete (7 Days)

Emails from Blocked senders are quarantined on arrival and automatically deleted after 7 days. This gives you a window to review false positives before permanent removal.

**How it works:** Blocked emails are flagged with a received timestamp. A cleanup cycle runs periodically and deletes any Blocked email older than 7 days.

**Why it matters:** Blocked senders do not accumulate in your inbox, but you have a safety net before anything is permanently gone.

### Action Email Auto-Delete

Processed action emails are removed from your inbox automatically. Deletion is verified by matching the 12-character security code, ensuring only the correct action email is removed.

**How it works:** After an action email response is processed and validated, the corresponding action email is located by its security token and deleted via IMAP.

**Why it matters:** Action emails are disposable by design. They serve their purpose and disappear. Your inbox is never cluttered with expired control messages.

### Persistent SMS Deduplication

Relegate tracks every SMS alert it sends and never sends the same alert twice, even across service restarts.

**How it works:** A persistent deduplication log records sent SMS alerts by email ID and alert type. On each processing cycle (and on startup lookback), the log is checked before any SMS is sent.

**Why it matters:** A service restart does not flood your phone with duplicate texts for emails already processed.

---

## 13. Configuration

Relegate stores all settings in local JSON files. No cloud accounts. No subscription portals. No data leaves your machine except the API calls you configure (Anthropic, Textbelt, Google Calendar, security services).

### All Local JSON

Every setting — sender roles, standing instructions, quiet hours, digest schedule, API keys — lives in JSON files on your local filesystem.

**How it works:** Configuration is read from JSON files at startup and watched for changes. Edits take effect on the next processing cycle.

**Why it matters:** Your email management rules, sender list, and preferences are files you own and control. Back them up, version them, or edit them in any text editor.

### GideonMail Compatible

Relegate uses the same configuration format as GideonMail. Migrating from GideonMail to Relegate (or running both) requires copying your config file.

**How it works:** The configuration schema is identical. A GideonMail config file is a valid Relegate config file with no modifications.

**Why it matters:** If you are already running GideonMail, switching to Relegate as a background service is a one-file migration.

---

*Built on the [GideonMail](https://github.com/gbroeckling/gideonmail) engine. Every feature listed here is available today.*
