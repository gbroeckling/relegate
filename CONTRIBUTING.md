# Contributing to Relegate

Thanks for your interest in contributing to Relegate! This is a background
Windows service for AI-powered email management -- triage, SMS alerts, calendar
integration, and sender management, all running locally on your machine.

## Current Status

Relegate is in **pre-release development** with a beta target of **June 1, 2026**.
The core features are being built and tested in
[GideonMail](https://github.com/gbroeckling/gideonmail), the Electron desktop
companion app. Relegate will share the same engine but run as a headless Windows
service with a web dashboard.

## How to Help

- **Test GideonMail** -- Install [GideonMail](https://github.com/gbroeckling/gideonmail)
  and try the AI triage, SMS alerts, calendar integration, and sender management.
  Bugs found there get fixed in both projects.
- **Report bugs** -- File issues using the
  [Bug Report](https://github.com/gbroeckling/relegate/issues/new?template=bug_report.yml)
  template. For GideonMail-specific bugs, file against that repo; they will be
  fixed in both.
- **Request features** -- Open an issue describing your use case so we
  understand *why* the feature matters.
- **Improve docs** -- Typos, unclear instructions, missing troubleshooting
  steps -- all welcome as PRs.

## Reporting Bugs

Use the [Bug Report](https://github.com/gbroeckling/relegate/issues/new?template=bug_report.yml)
issue template. Include:

- Your OS version and Node.js version
- Steps to reproduce
- Expected vs. actual behavior
- Any relevant log output

## Requesting Features

Use the [Feature Request](https://github.com/gbroeckling/relegate/issues/new?template=feature_request.yml)
template. Describe your use case -- what you are trying to accomplish and why
existing functionality does not cover it.

## Development Setup

1. Clone [GideonMail](https://github.com/gbroeckling/gideonmail) (the desktop
   app where active development happens):
   ```
   git clone https://github.com/gbroeckling/gideonmail.git
   cd gideonmail
   ```
2. Install dependencies:
   ```
   npm install
   ```
3. Start the app:
   ```
   npm start
   ```

GideonMail requires Node.js and an Electron-compatible environment. You will
need IMAP email credentials and a Claude API key to exercise the full feature
set.

## Code Style

- **JavaScript** -- No TypeScript. The project uses plain JavaScript throughout.
- **Electron** -- The main process lives in a single `main.js` file (~4000 lines)
  that handles IMAP, SMTP, AI, SMS, Calendar, and Security.
- **Single main.js pattern** -- All backend logic is co-located in one file for
  simplicity. Utility modules (`security.js`, `google-auth.js`) are broken out
  only when they serve a distinct purpose.
- Keep code readable. Match existing patterns and naming conventions.

## Pull Request Process

1. **Fork** the repository and create a feature branch from `main`.
2. **Branch naming** -- Use descriptive names like `fix/imap-reconnect` or
   `feature/quiet-hours`.
3. **Describe** your changes in the PR -- what changed, why, and how to test it.
4. **Test** your changes against a running GideonMail instance before submitting.
5. Keep commits focused -- one logical change per commit.
6. A maintainer will review and merge when ready.

## How This Project Is Built

Relegate is built by [Garry Broeckling](https://github.com/gbroeckling). All
architecture, product decisions, testing, and releases are human-directed.
Implementation is AI-assisted using [Claude](https://claude.ai) by Anthropic,
which accelerates the write-test-ship cycle considerably.

If you contribute a PR, there is no requirement to use (or not use) AI tools.
Write code however you are most productive -- what matters is that it works,
follows the existing patterns, and passes review.

## Code of Conduct

Please read our [Code of Conduct](CODE_OF_CONDUCT.md). Be kind, be
constructive. We are all here to make email management better.
