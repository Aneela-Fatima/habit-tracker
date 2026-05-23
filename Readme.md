# Habit Tracker
# Streaks — Habit Tracker

A clean, minimal habit tracker with weekly streaks.  
Built with vanilla HTML, CSS, and JavaScript — no framework, no build step.

## How to run locally

Open `index.html` directly in any modern browser:

```bash
# Option 1 — just double-click index.html in File Explorer

# Option 2 — local dev server (optional)
python3 -m http.server 8080
# then open http://localhost:8080
```

**Requirements:** Any modern browser (Chrome 90+, Firefox 88+, Safari 14+). No installs needed.

## Deployed URL

🔗 https://habit-tracker-ashen-three.vercel.app/

## Project structure
habit-tracker/

├── index.html     ← entire app (HTML + CSS + JS)

├── README.md      ← setup instructions

└── ANSWERS.md     ← design and process notes

## Features

- Add, rename (double-click), and delete habits
- Weekly grid: habits as rows, 7 days as columns
- Toggle checkmarks per day
- Today's column is always highlighted
- Streak counter per habit (consecutive days)
- Week navigation: prev / next / back to today
- Historical data persists across page reloads (localStorage)
- Empty state when no habits exist
- Responsive from 360px phone to 1440px desktop
- Automatic dark mode (follows OS preference)
