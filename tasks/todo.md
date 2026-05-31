# Flip 7 Scorer — Feature Plan

## STATUS: ✅ All 4 shipped & verified live (2026-05-31)
- Settings + custom target (100/150/200/custom) — tested
- Game history + all-time leaderboard (separate localStorage) — tested
- End-of-game highlights (biggest round / most Flip 7s / most busts) — tested
- Player colors + avatar chips + medals — tested
- Future idea: "Flip 7 with a Vengeance" mode (negative scores, steal points) — needs its own card set, deferred.


## Context
- Official rules confirmed: scoring is correct; first to 200 wins; no separate rule variants.
- Practical "variation" = configurable winning score.
- Competitor (boardgamehelpers.com) is a bare manual score table — we already exceed it.

## Planned features

### 1. Settings (rule variations) ⚙️
- Settings modal (gear icon in header).
- Winning score target: presets 100 / 150 / 200 (default) / custom number.
- Replace hard-coded TARGET=200 with state.target everywhere (win detection, banner, winner modal).
- Sound toggle moves into settings too (declutter header).

### 2. Game history + all-time leaderboard 🏆
- Separate localStorage key `flip7-history-v1` (independent of the live game).
- On game end (someone reaches target), auto-save a record:
  { date, target, rounds, players:[{name,total,flip7s,busts}], winnerName }.
- History view (clock/trophy icon):
  - All-time leaderboard: wins, games played, best game, total Flip 7s per player name.
  - List of past games (date · winner · final scores), tap to expand round detail.
  - "Clear history" (with styled confirm).

### 3. End-of-game fun stats 🎉
- In the winner modal, show fun highlights from the game:
  - Most Flip 7s, biggest single round (+who), most busts, closest finish.
- Keeps the celebration feeling rewarding.

### 4. Player colors / avatars 🎨
- Auto-assign each player a distinct accent color + initial chip.
- Used on player rows, scoreboard, winner podium — adds life.

## Build / verify
- Edit single index.html (vanilla, no deps).
- localStorage migration-safe (default target, history key optional).
- Test in browser via Playwright: settings target change, full game → auto history record, leaderboard aggregation, stats correctness.
- Commit + push (auto-deploys to Vercel). Verify live.

## Notes
- Date.now() is fine here (browser, not a workflow script).
- Keep it phone-first and simple — don't over-engineer.
