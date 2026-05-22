# Answers
# ANSWERS.md

## 1. How to run

No build step required. Open `index.html` in any modern browser:

```bash
# Double-click index.html
# or run a local server:
python3 -m http.server 8080
```

**Deployed URL:** https://habit-tracker-rust-phi-62.vercel.app/

---

## 2. Stack & design choices

**Stack:** Vanilla HTML/CSS/JS — single file, no framework, no build toolchain.

Chosen because the spec judges information design above all else. A framework adds zero design leverage here while making the submission harder to run. A single `index.html` opens instantly with no setup that can fail on a reviewer's machine.

**Visual decision 1 — Fixed-width day columns (40px), not fluid**

The seven day columns are fixed at 40px each. I rejected fluid (`1fr`) columns because the grid's job is visual comparison across time — your eye needs to sweep a row and instantly spot gaps in a streak. If columns flex with content, the spatial rhythm breaks and the grid loses its calendar-like regularity. The habit name column takes all leftover space instead, since names vary in length but day widths don't need to.

**Visual decision 2 — Full-column today highlight, not just a date badge**

Today's column gets a solid green header and a faint green tint on every cell below it. The common alternative — circling the date number — makes you scan the header to find today. A full-column treatment lets your eye jump straight to today on load, which matters every single time you open the app.

**Week starts Monday.** Weekend (Sat–Sun) clusters naturally at the right edge as a visual block. A Sunday start splits the week awkwardly and buries the weekend in the middle.

---

## 3. Responsive & accessibility

**360px phone:** Day columns shrink from 40px to 32px. Habit names truncate with ellipsis. Week nav wraps to a second line. The grid stays a true grid — I did not collapse it to cards, because losing the grid means losing the at-a-glance streak view, which is the core value of the app.

**1440px desktop:** Layout is capped at 900px and centered. Extra space goes into the habit name column.

**Accessibility handled — keyboard navigation:** Every checkmark cell has `tabindex="0"` and responds to Enter and Space, so the full grid is keyboard-navigable. Add-habit submits on Enter. Rename commits on Enter, cancels on Escape. Delete buttons have `aria-label` attributes.

**Accessibility skipped — ARIA grid role:** The grid is div-based, not a proper `role="grid"` with `role="gridcell"`. A full ARIA grid would let screen readers navigate with arrow keys like a spreadsheet. Skipped because correct focus management across a dynamic grid is a significant implementation — it would have consumed most of the available time. A production version would use a proper `<table>` or full ARIA grid semantics.

---

## 4. AI usage

**Tool:** Claude (Anthropic)

1. **Grid layout** — Asked for a weekly grid with habits as rows and days as columns. AI gave equal `1fr` columns for everything. I changed day columns to fixed `40px` and gave only the habit name `1fr`, because equal columns gave too much space to short day labels and not enough visual rhythm for scanning streaks horizontally.

2. **Streak logic** — AI calculated streaks always starting from today. I changed it to start from yesterday when today is unchecked. Reason: at 9 AM before completing a habit, the streak should show yesterday's intact run — not drop to zero — because the day isn't over yet.

3. **Dark mode** — AI gave a toggle button with a `[data-theme]` attribute. I replaced it with `@media (prefers-color-scheme: dark)` and CSS custom properties, removing the toggle entirely. The OS preference is the right source of truth; an in-app toggle creates a setting the user has to maintain separately.

---

## 5. Honest gap

**The rename interaction has no affordance.**

Double-clicking a habit name triggers rename, but nothing tells the user this is possible. The delete button appears on hover, so deletion is at least discoverable. Renaming is invisible. With another day I would add a pencil icon (appearing on hover next to the delete button) and replace the blur-to-commit behavior with explicit ✓ / ✕ buttons — because silently committing on blur is surprising when you click elsewhere.
