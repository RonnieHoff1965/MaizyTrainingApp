# Maizy's Training App

A complete hunting dog training schedule app for **Maple Run's Marsh Maiden** — Call Name: **MAIZY** (born February 13, 2026).

## Live App

**URL:** https://ronniehoff1965.github.io/MaizyTrainingApp/maizy_app_2.html

> Login required. Contact the owner for access.

## Features

- **Dashboard** — Real-time age tracking, training progress gauge (0–100%), critical milestone timeline
- **Training** — Week-by-week training plan (Weeks 8–48), goal checklists, Stonnie Dennis techniques, daily training log
- **History** — Full log of completed weeks, daily entries, and notes
- **Resources** — Recommended books and online content (Stonnie Dennis YouTube, etc.)

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Single-file HTML/CSS/JS (vanilla) |
| Hosting | GitHub Pages (public repo, free) |
| Authentication | Supabase Auth (email + password) |
| Database | Supabase Firestore (cloud-synced across all devices) |

## Authentication

- Single user app — password protected via Supabase Auth
- Login required before any content is visible
- Logout button in top-right corner of app
- Forgot password flow built into the login screen
- Data syncs across all devices automatically after login

## Data Storage

- Training data stored in **Supabase** (`training_data` table, `jsonb` column)
- `localStorage` used as offline cache/fallback
- Row-Level Security enabled — only the authenticated user can read/write their data

## Supabase Project

- **Project:** RonnieHoff1965's Project
- **Region:** West US (Oregon)
- **Project Ref:** `ayebupzaaibodhvigwez`
- **Dashboard:** https://supabase.com/dashboard/project/ayebupzaaibodhvigwez

## Deployment

All changes are deployed automatically via GitHub Pages on every push to `main`.

To push an update:
```bash
git add maizy_app_2.html README.md CLAUDE.md
git commit -m "Description of change"
git push
```

GitHub Pages typically deploys within 60 seconds of a push.

## Training Schedule Overview

| Phase | Weeks | Key Focus |
|---|---|---|
| Foundation | 8–12 | Name, crate, basic commands, socialization |
| Gunfire & Water | 13–16 | Gunfire imprinting, first swims, recall |
| Retrieving | 17–24 | Bumper retrieves, live bird introduction |
| Advanced | 25–36 | Force fetch, e-collar conditioning |
| Started Level | 37–48 | No food treats, field work, first Started test |
