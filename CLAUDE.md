# CLAUDE.md — NetO Coaching Income Tracker

## What This Project Is

NetO is a PWA (Progressive Web App) coaching income tracker built for Nero — a tennis and padel coach operating across the US, Argentina, and The Bahamas. It tracks session income, tips, and match fees. It auto-calculates earnings from a user-defined rate card. It supports multiple coaches (multi-user) via username + PIN authentication.

The current deployed version is **NetO v3**, hosted on Netlify as a static site.

-----

## Stack

- **Language:** Vanilla HTML, CSS, JavaScript — no framework, no build tools
- **Dependencies:** Google Fonts via CDN only
- **Architecture:** Single-file app (`index.html`)
- **Storage:** `localStorage` — all data lives on the user’s device, per browser
- **Backend:** None. No server. No database. No API calls.
- **Deployment:** Netlify static hosting

-----

## What This App Does

- Multi-user login: username + PIN authentication stored in localStorage
- Session logging: type (tennis/padel/match), duration, tip, auto-calculated income
- Rate card: user-defined rates per session type
- Weekly/monthly/summer goal tracking
- Coach report: best day, slowest day, $/hr efficiency by session type
- Week counter anchored to account creation date
- PWA: installable on iOS and Android via “Add to Home Screen”

-----

## Architecture Rules

- **One file only.** All HTML, CSS, and JS lives in `index.html`. Do not split into separate files unless explicitly instructed.
- **No frameworks.** Do not introduce React, Vue, Alpine, or any JS framework. Ever.
- **No build tools.** No Webpack, Vite, npm, or package.json. This is a static file.
- **No backend.** Do not suggest APIs, servers, databases, or cloud storage. localStorage is the intentional choice.
- **No new CDN dependencies** without explicit approval. Google Fonts is the only external dependency.

-----

## localStorage Schema

All data is namespaced by username to support multi-user. Do not flatten or restructure keys without a migration plan.

Key patterns:

- `neto_users` — array of registered user objects
- `neto_sessions_{username}` — array of session log entries per user
- `neto_settings_{username}` — rate card and preferences per user
- `neto_goals_{username}` — weekly/monthly/summer goal targets per user

**Rules:**

- Never rename or restructure existing keys without writing a migration function
- Never clear localStorage without explicit user action
- Always check if a key exists before reading; default gracefully if null

-----

## Current State

- Deployed and tested on Edge desktop
- localStorage confirmed working
- Week counter anchored to account creation date
- **No GitHub repo yet** — code lives in Claude conversation history
- Latest version: NetO v3

-----

## Next Steps Planned

1. Language toggle (English / Spanish)
1. Week 1 historical data migration for original user
1. Eventual App Store submission (PWA wrapper)

-----

## Do Not Do

- Do not add a backend or suggest migrating to one unless explicitly asked
- Do not split the single file into multiple files
- Do not rename localStorage keys without a migration function
- Do not introduce any JS framework or build toolchain
- Do not add CDN dependencies without approval
- Do not rewrite sections of the app that aren’t part of the current feature
- Do not assume the rate card structure — always read the existing schema first

-----

## Before Every Feature

1. Read the full current `index.html` before writing a single line
1. Map which functions and localStorage keys the feature will touch
1. Identify what currently works that could break
1. Flag any risk (data migration, multi-user edge cases, PWA manifest impact)
1. Get approval on the plan before writing code

-----

## When Something Breaks

- Do not patch over it by adding more code
- Identify the root cause first
- If the wrong assumption is deep in the conversation context, start a fresh session with the correct assumption in the first prompt
- A clean session beats a patched session every time

-----

## Language Toggle (Upcoming)

- All user-facing strings must eventually support EN and ES
- When adding new UI text, add it to the strings object — do not hardcode text directly into HTML
- Do not start the language toggle implementation until explicitly asked

-----

## PWA Rules

- Do not modify the service worker or manifest without understanding caching implications
- Manifest changes require a retest of “Add to Home Screen” on both iOS and Android
- Cache versioning must be bumped when assets change
