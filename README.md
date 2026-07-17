# Seams

**Projects die between sessions — track the gaps.**

Seams is a single-file project command center. Every project is an inspection tag on a board: its phase, the one concrete next action, what's blocking it, and a **drift gauge** that fills as days pass without you touching the project — turning amber, then stamping the card **STALE**. The point isn't tracking what you did; it's making the gaps between work sessions visible before a project quietly dies in one.

No build, no dependencies, no server. One `index.html`. Data lives in your browser's localStorage.

## Use it

**Live:** https://madfoosa.github.io/Seams/

Or just download `index.html` and open it in a browser — that's the whole app.

## Features

- **Inspection-tag board** — each project card shows phase (Idea → Planning → Building → Pilot → Paused → Shipped), tags, next action, and blockers, sorted so the most-neglected active work surfaces first.
- **Drift gauge** — configurable per project: how many untouched days until amber, how many until STALE.
- **Session log** — "Log a session" records what happened and resets the drift gauge. **Mark touched** resets the gauge without a log entry.
- **Search & filter** — filter the board by text, phase, or stale-only.
- **Handoff briefs** — one click generates a paste-ready markdown brief for resuming a project in a fresh AI chat: phase, next action, blockers, standing decisions, artifacts to upload, and recent log.
- **JSON import/export** — the exported file is the source of truth and is safe to hand to an agent or another machine; re-import to sync.

## Working with agents

Two built-in bridges to AI-assisted work:

1. **Copy full brief for an agent** (toolbar) — copies the entire board as markdown-wrapped JSON, with instructions for the agent to return updated state in the same schema for re-import.
2. **Handoff** (per card) — copies a focused resume-this-project brief for a fresh chat.

### Export schema

```
{
  version, exported_at,
  projects: [{
    id, name, phase, next_action, blockers,
    artifacts[], tags[], notes,
    log: [{at, entry}],
    created_at, touched_at,
    drift_amber_days, drift_stale_days
  }]
}
```

An agent (or you) can edit the JSON directly and re-import it. Imports are validated: unknown phases, malformed dates, and junk fields are sanitized rather than breaking the board.

## Privacy

Everything stays in your browser. There is no backend, no analytics, no network calls beyond loading fonts.
