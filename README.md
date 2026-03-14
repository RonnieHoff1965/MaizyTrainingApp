# Maizy's Training App

A complete hunting dog training schedule app for **Maple Run's Marsh Maiden** — Call Name: **MAIZY** (born February 13, 2026).

## Live App

**URL:** https://ronniehoff1965.github.io/MaizyTrainingApp/maizy_app_2.html

> Login required — password protected via Supabase Auth.

---

## Features

### 🏠 Dashboard
- Real-time age tracking (days, weeks, months)
- Training progress gauge (0–100%) with speedometer
- **🔥 Training Streak Counter** — consecutive days logged
- **🎯 Next Milestone Countdown** — days until next critical training event
- **📊 Weekly Progress Bar Chart** — visual completion across all 41 weeks
- **📋 Training Report Cards** — 10 phase grade blocks (A–F) with progress bars; future phases show 🔒 locked with available date
  - Foundation · Early Obedience · Retrieving Basics · Bird & Water Work
  - Advanced Field · Retrieve Mastery · Desire Training · E-Collar & Marks
  - Started Level Prep · Hunt Test Ready
- Critical milestone timeline
- Treat transition timeline

### 🎯 Training (Weeks 8–48)
- Week-by-week training plan following **Stonnie Dennis method** (desire-based, no force fetch)
- Goal checklists with progress tracking (0–25–50–75–100%)
- Stonnie Dennis techniques for each week
- Socialization checklists
- **⚠️ Carry-Forward Goals** — automatically surfaces incomplete goals from past 4 weeks
- **Daily Training Log** with:
  - ⏱️ Built-in session timer (stopwatch) — duration saved with each entry
  - 🌤️ Weather conditions (Sunny/Cloudy/Rainy/Windy/Hot/Cold) + temperature °F
  - 📷 Photo attachment — resize & store photos with each log entry
  - Date picker for back-logging sessions
- **📋 Weekly Report Card** — per-week grade, all goals, logs, photos, and notes
  - Print / Save as PDF button built in
- Week summary notes
- Mark week complete

### 📜 History
- Full log of all completed weeks
- Daily entries with weather, photos, duration, and notes
- Sorted newest-first

### 📚 Resources
- Recommended books and YouTube content (Stonnie Dennis, etc.)

---

## Training Philosophy

All training follows **Stonnie Dennis's desire-based method**:
- Dog retrieves because it **loves it** — never because it's forced
- No ear pinch, no toe hitch, no force methods
- Short happy sessions (5–10 min), always end on success
- If dog hesitates → stop, rebuild desire, never correct
- E-collar introduced only after commands are solid and willing, as communication not punishment

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Single-file HTML/CSS/JS (vanilla, no build step) |
| Hosting | GitHub Pages (main branch, free) |
| Authentication | Supabase Auth (email + password) |
| Database | Supabase (`training_data` table, jsonb) |
| Offline | localStorage cache + fallback |

---

## Authentication

- Single-user app — password protected
- Login required before any content is visible
- Forgot password / reset password built into the login screen
- Data syncs across all devices automatically after login

---

## Supabase Project

- **Project Ref:** `ayebupzaaibodhvigwez`
- **Region:** West US (Oregon)
- **Dashboard:** https://supabase.com/dashboard/project/ayebupzaaibodhvigwez
- **Table:** `training_data` — columns: `id`, `user_id`, `data` (jsonb), `updated_at`
- **RLS:** enabled — only authenticated user can read/write

---

## Deployment

Push to `main` → GitHub Pages deploys in ~60 seconds.

```bash
git add maizy_app_2.html README.md CLAUDE.md
git commit -m "Description of change"
git push
```

---

## Training Schedule Overview

| Phase | Weeks | Key Focus |
|---|---|---|
| Foundation | 8–11 | Name, crate, basic commands, socialization |
| Early Obedience | 12–15 | Gunfire imprinting, first swims, recall, leash |
| Retrieving Basics | 16–19 | Bumper retrieves, treat transition, live birds |
| Bird & Water Work | 20–23 | First live bird, water proficiency, doubles |
| Advanced Field | 24–27 | Blinds, casting, advanced marking, desire building |
| Retrieve Mastery | 28–31 | Hold/fetch/give — desire-based, no pressure |
| Desire Training | 32–35 | Stonnie Dennis retrieve mastery (4 phases) |
| E-Collar & Marks | 36–39 | E-collar conditioning, all commands solid |
| Started Level Prep | 40–43 | No food treats, field work, test-ready skills |
| Hunt Test Ready | 44–48 | First Started test at 12 months |
