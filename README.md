# StudyDeck

A single-file study dashboard that runs entirely in the browser. No build step, no server, no account. Open the HTML file and it works.

Notes, spaced-repetition flashcards, a project planner, a schedule, and a plan-of-study view, all persisted to `localStorage`.

> Built collaboratively with an AI assistant. The design decisions, feature scope, and behaviour rules are mine; much of the implementation was generated and then reviewed against them.

## Quick start

```
git clone https://github.com/YOUR-USERNAME/studydeck.git
cd studydeck
open StudyDeck.html          # macOS
start StudyDeck.html         # Windows
xdg-open StudyDeck.html      # Linux
```

That is the whole install. To use it day to day, bookmark the local file or host it on GitHub Pages.

> **Storage lives in your browser.** Everything is saved to `localStorage`, which is per-browser and per-device, and clearing site data erases it. Use the JSON export regularly.

## What it does

**Notes** — a block editor with headings, lists, to-dos, code blocks, tables, callouts, and images. Pages nest into a tree. Split view opens up to three pages side by side, each scrolling independently. Typing `/` in any block opens a type menu.

**Auto-formatting** — `2^2` becomes a superscript, `V_out` a subscript, `\tau` becomes τ, `->` becomes →. Around 150 shortcuts, converted as you type. Code blocks are never touched, and the rules deliberately leave `snake_case`, `MAX_CONSTANTS`, and Python operators like `!=` and `<=` alone.

**Flashcards** — Leitner-box spaced repetition across six boxes. Optional typed answers, self-grading, session stats, CSV export, and a built-in deck library.

**Projects** — steps with due dates, prerequisites, notes, and progress tracking.

**Schedule, plan of study, grades, resources** — weekly timetable, multi-term course planner with credit totals, and a GPA calculator.

## Making it yours

Everything below is plain data near the top of the relevant section in `StudyDeck.html`.

| What | Where |
|---|---|
| Terms and courses | `ACADEMIC_PLAN` |
| Flashcard decks | `FC_LIBRARY` |
| Symbol and emoji shortcuts | `NL_SYMBOLS` |
| Colour scheme | CSS variables in `:root` |

The bundled decks and lesson pages are an example set aimed at introductory programming, circuits, digital logic, and semiconductors. Delete them from the Library panel, or replace `FC_LIBRARY` with your own.

## Data and privacy

Nothing leaves your machine. There is no analytics, no telemetry, and no network request of any kind. Use **Export JSON** for backups and **Import** to restore or move between devices.

## Browser support

Any current Chrome, Firefox, Safari, or Edge. It uses `contenteditable`, the Selection API, and `localStorage`, so it will not work in a browser with JavaScript disabled.

## Project size

Roughly 23,000 lines in one file: about 600 functions and 540 CSS rules across 23 panels. One file is a deliberate constraint — it means the app can be emailed, dropped on a USB stick, or opened from a downloads folder years later with no toolchain to resurrect.

The tradeoff is real. There is no module system, no tests, and no minification. If you are looking for a well-architected codebase to learn from, this is not that. If you want a study tool that will still open in 2035, it is.

## Design decisions

A few rules in here are deliberate and took more than one attempt to get right.

**Subscripts require a single-letter base.** `V_out` and `X_C` convert; `my_list`, `is_even`, `student_count`, and `MAX_CREDITS` do not. Physics notation and Python identifiers look alike, and a two-letter base swallowed the second group. An all-caps tail of three or more is also skipped so `N_SAMPLES` stays a constant.

**`<=`, `>=`, and `!=` never auto-convert.** They are real operators, and silently turning them into glyphs inside a programming note is worse than not converting at all. Those need an explicit `\le`, `\ge`, `\ne`.

**Arrows need whitespace on both sides.** Without that rule, `if x <-5` becomes `if x ←5`. A comparison against a negative number is far more likely than an arrow jammed against a digit.

**Blocks resolve their page from their own ID, not from a global.** That is what makes split panes editable rather than read-only: a block always belongs to its own page regardless of which pane renders it.

**Deleted seeded content stays deleted.** Removing a bundled deck or lesson records a tombstone, so no seeding pass ever restores it and the storage stays freed.

## Contributing

Issues and pull requests are welcome. Because it is one file, please keep diffs tight and describe the change in the PR body.

## Licence

MIT. See [LICENSE](LICENSE).
