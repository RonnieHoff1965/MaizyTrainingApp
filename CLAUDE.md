# CLAUDE.md — Maizy Training App

Instructions and context for Claude when working on this project.

## Project Overview

Single-file HTML app (`maizy_app_2.html`) for tracking Maizy's hunting dog training schedule. All app logic, styles, and HTML are in one file (~3,500+ lines).

## Key Rule: Update Docs on Every Push

**Before every `git push`, always update:**
- `README.md` — reflect any new features, changes to stack, or URL changes
- `CLAUDE.md` — update architecture notes if anything structural changed

## Architecture

- **One file:** `maizy_app_2.html` contains all HTML, CSS (~1,250 lines), and JS (~2,200 lines)
- **Data:** `appData` object synced to Supabase + cached in `localStorage`
- **Auth:** Supabase Auth — `db.auth.onAuthStateChange()` drives app startup
- **No build step** — edit the file, push, done

## Critical Functions

| Function | Location | Purpose |
|---|---|---|
| `loadData()` | ~line 3390 | Async — loads from Supabase (5s timeout), falls back to localStorage |
| `saveData(data)` | ~line 3408 | Sync localStorage + async Supabase upsert (fire-and-forget) |
| `initApp()` | ~line 3418 | Async — called after auth, loads data and renders all views |
| `updateDashboard()` | mid-script | Renders header stats, progress gauge, speedometer |
| `renderWeekContent(week)` | mid-script | Renders training content for selected week |
| `renderHistory()` | mid-script | Renders history tab |
| `switchView(name)` | mid-script | Switches between dashboard/training/history/resources tabs |

## Auth Flow

```
Page load → loadingOverlay shown
  ↓
onAuthStateChange fires
  ├── PASSWORD_RECOVERY → hide loading, show resetBox
  ├── session exists → hide loginOverlay, show loading, initApp(), hide loading
  └── no session → hide loading, show loginOverlay
```

## Supabase Config

- **URL:** `https://ayebupzaaibodhvigwez.supabase.co`
- **Anon key:** in `maizy_app_2.html` near top of `<script>` block (`SUPABASE_ANON_KEY`)
- **Table:** `training_data` — columns: `id`, `user_id`, `data` (jsonb), `updated_at`
- **RLS:** enabled — policy: `auth.uid() = user_id`
- **User:** `Ronniehoff1965@gmail.com`

## GitHub & Deployment

- **Repo:** https://github.com/RonnieHoff1965/MaizyTrainingApp (public)
- **Live URL:** https://ronniehoff1965.github.io/MaizyTrainingApp/maizy_app_2.html
- **Hosting:** GitHub Pages from `main` branch root
- **Deploy time:** ~60 seconds after push

## Making Edits

Since the file is large (100KB+), use the Bash tool with Python for string replacements:
```bash
cd "/Users/ronniehoff/Documents/Claude Projects/Maizy Training APP" && python3 - <<'PYEOF'
with open('maizy_app_2.html', 'r') as f:
    content = f.read()
content = content.replace('OLD TEXT', 'NEW TEXT', 1)
with open('maizy_app_2.html', 'w') as f:
    f.write(content)
PYEOF
```

The Edit tool may fail on this file due to size — always prefer the Python approach.

## Preview Server

Launch config is in `.claude/launch.json`. Serves from `/tmp/` due to macOS sandbox restrictions.
To preview: copy file to `/tmp/`, then use `preview_start "Maizy Training App"`.

## User Preferences

- Update README.md and CLAUDE.md on every push
- Keep docs reflecting current state of the app
