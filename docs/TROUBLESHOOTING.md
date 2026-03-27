# Troubleshooting

Common issues and their solutions for GideonMail and Relegate.

## IMAP Connection Drops (ECONNRESET)

**Symptom:** "Connection reset" or "ECONNRESET" errors in the log.

**Cause:** The IMAP server closed the connection due to inactivity, server
restart, or network interruption.

**Solution:** The app handles this automatically -- it detects the dropped
connection and reconnects. If drops are frequent, check your network stability
and whether your email provider has aggressive idle timeouts. No user action is
required in most cases.

## "Download returned empty"

**Symptom:** Fetching an email body returns empty content.

**Cause:** Usually a stale IMAP connection where the server has silently
dropped the session but the client has not yet detected it.

**Solution:** The app retries automatically with a fresh IMAP client. If this
persists for specific emails, the message may have been deleted server-side or
may use an encoding the parser cannot handle. Try refreshing the mailbox.

## Self-Signed Certificates

**Symptom:** IMAP or SMTP connection fails with certificate errors when
connecting to a self-hosted mail server.

**Cause:** The server uses a self-signed or internally-issued TLS certificate
that Node.js does not trust.

**Solution:** The app sets `tls.rejectUnauthorized = false` for IMAP connections
to handle this. If you are still seeing certificate errors, verify your server's
TLS configuration and ensure the correct port is configured (993 for IMAPS, 465
or 587 for SMTP).

## IMAP Search Failures on ISPConfig

**Symptom:** Email search returns errors or no results on ISPConfig-hosted mail
servers.

**Cause:** Some ISPConfig/Dovecot configurations do not support complex compound
IMAP SEARCH commands or certain search criteria combinations.

**Solution:** The app uses simplified sequential search on these servers --
breaking compound searches into individual steps. If search still fails, check
that your Dovecot full-text search (FTS) plugin is properly configured.

## Lock Contention

**Symptom:** Operations hang or timeout when multiple actions run simultaneously
(e.g., fetching emails while searching).

**Cause:** The shared IMAP client can only process one command at a time. If two
operations try to use it simultaneously, one blocks.

**Solution:** The app creates fresh IMAP clients for parallel operations. If you
are seeing contention, it may indicate a code path that is not using a fresh
client when it should -- file a bug report with the operation you were performing.

## SMS Not Sending

**Symptom:** SMS alerts are not delivered despite being configured.

**Possible causes and solutions:**

- **Textbelt API key** -- Verify your key is correct and active in Settings.
  Test it at [textbelt.com](https://textbelt.com).
- **Rate limits** -- Textbelt limits sending frequency. If you have sent many
  messages recently, you may be rate-limited. Wait and try again.
- **Quiet hours** -- Check if quiet hours are enabled and currently active. SMS
  alerts are suppressed during quiet hours by design.
- **Phone number format** -- Ensure the number includes the country code
  (e.g., +1 for US).

## Calendar Not Connecting

**Symptom:** Google Calendar integration fails or stops working.

**Possible causes and solutions:**

- **Expired OAuth tokens** -- Google OAuth refresh tokens can expire if unused
  for extended periods or if you change your Google password. Re-authorize the
  connection in Settings.
- **Revoked access** -- Check your Google account's third-party app permissions
  at [myaccount.google.com/permissions](https://myaccount.google.com/permissions).
- **API quota** -- Google Calendar API has daily request limits. If you are
  processing a very high volume of emails, you may hit the quota.

## Low Touch Not Processing

**Symptom:** Low Touch mode is configured but emails are not being automatically
processed.

**Checklist:**

- **Enabled?** -- Low Touch must be explicitly enabled in Settings. It is off
  by default.
- **API key?** -- Low Touch requires a valid Claude API key. Check that it is
  entered and working.
- **Email criteria** -- Low Touch only processes emails that match its configured
  criteria. Verify your rules are set up correctly.
- **Check logs** -- Look for AI triage errors that may indicate API failures or
  rate limiting.

## GPU Cache Errors on Startup

**Symptom:** Errors referencing GPU cache, shader cache, or "Dawn" appear in
the console on startup.

**Cause:** These are harmless Chromium/Electron messages caused by rapid
restarts or stale cache files. They do not affect functionality.

**Solution:** No action needed. These can be safely ignored. If they bother you,
deleting the app's GPU cache directory and restarting will clear them.

## Windows Notifications Not Showing

**Symptom:** Desktop notifications (new email alerts, SMS confirmations) do not
appear on Windows.

**Cause:** Windows requires the app to have an Application User Model ID
(AppUserModelId) registered to show notifications. When running via `npm start`
during development, this ID may not be registered.

**Solution:** Install the app using the packaged installer (when available)
rather than running from source. The installed version registers the correct
AppUserModelId. During development, notifications may not appear -- this is a
known limitation of running Electron apps in dev mode on Windows.
