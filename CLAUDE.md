# CLAUDE.md — Maizy Training App

Instructions and context for Claude when working on this project.

## Project Overview

Single-file HTML app (`maizy_app_2.html`) for tracking Maizy's hunting dog training schedule. All app logic, styles, and HTML are in one file (~4,000+ lines).

## Key Rule: Update Docs on Every Push

**Before every `git push`, always update:**
- `README.md` — reflect any new features, changes to stack, or URL changes
- `CLAUDE.md` — update architecture notes if anything structural changed

## Architecture

- **One file:** `maizy_app_2.html` contains all HTML, CSS (~1,500 lines), and JS (~2,500 lines)
- **Data:** `appData` object synced to Supabase + cached in `localStorage`
- **Auth:** Supabase Auth — `db.auth.onAuthStateChange()` drives app startup
- **No build step** — edit the file, push, done

## Critical Functions

| Function | Location | Purpose |
|---|---|---|
| `loadData()` | ~line 3400 | Async — loads from Supabase (5s timeout), falls back to localStorage |
| `saveData(data)` | ~line 3420 | Async IIFE upsert + sync localStorage |
| `initApp()` | ~line 3430 | Async — called after auth, loads data and renders all views |
| `updateDashboard()` | mid-script | Renders header stats, gauge, streak, milestone, chart, grade blocks |
| `renderWeekContent(week)` | mid-script | Renders training content + carry-forward goals |
| `renderHistory()` | mid-script | Renders history tab |
| `switchView(name)` | mid-script | Switches between dashboard/training/history/resources tabs |
| `showReportCard(week)` | mid-script | Opens report card modal for a given week |
| `renderGradeBlocks()` | mid-script | Renders 10 phase grade cards on dashboard |
| `getCarryForwardGoals(week)` | mid-script | Returns incomplete goals (<70%) from past 4 weeks |
| `calcStreak()` | mid-script | Calculates consecutive training days |
| `getNextMilestone()` | mid-script | Returns next uncompleted milestone |
| `renderProgressChart()` | mid-script | Renders bar chart of all 41 weeks |
| `timerStart/Stop/Reset()` | mid-script | Session timer on training page |
| `handlePhotoSelect(input)` | mid-script | Resizes + encodes photo to base64 |
| `selectWeather(btn)` | mid-script | Toggles weather condition selection |

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

## Training Philosophy

All training data follows **Stonnie Dennis desire-based method**:
- No force fetch, no ear pinch, no toe hitch
- Weeks 32–35 use desire-based retrieve mastery (4 phases)
- E-collar introduced as communication tool, not punishment

## appData Structure

```json
{
  "startDate": "ISO date string",
  "currentWeek": 8,
  "completedWeeks": [8, 9, 10],
  "weekData": {
    "8": {
      "completedGoals": [0, 1, 2],
      "goalProgress": { "0": 100, "1": 75 },
      "notes": "week notes",
      "date": "ISO date",
      "dailyLogs": [
        {
          "date": "YYYY-MM-DD",
          "entry": "log text",
          "weather": "☀️ Sunny",
          "temp": "65",
          "duration": "00:25:00",
          "photo": "data:image/jpeg;base64,...",
          "timestamp": "ISO date"
        }
      ]
    }
  }
}
```

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
- Training follows Stonnie Dennis method — no force fetch references
- Git user: Ronnie Hoff <Ronniehoff1965@gmail.com>
