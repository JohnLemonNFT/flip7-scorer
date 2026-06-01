# Flip 7 Scorer — Feature Plan

## STATUS: ✅ All 4 shipped & verified live (2026-05-31)
- Settings + custom target (100/150/200/custom) — tested
- Game history + all-time leaderboard (separate localStorage) — tested
- End-of-game highlights (biggest round / most Flip 7s / most busts) — tested
- Player colors + avatar chips + medals — tested
- ✅ "Flip 7: With a Vengeance" mode SHIPPED (2026-05-31): Classic/Vengeance toggle in Settings.
  Vengeance adds 13 + Lucky 13 cards, minus cards (−2..−10), Unlucky 7 reset, ± steal/penalty box,
  Flip 7 choice (+15 self / −15 rival), Brutal toggle (floor-at-0 vs negative). Unit + browser tested.
  Note: table-resolved actions (Steal/Swap/Discard/Flip Four/Just One More) net via the ± box by design.
  Minus-card denominations assumed −2..−10 (mirror of +mods); ± box covers any oddballs.

## Vengeance rules research (2026-05-31) — confirmed vs best-guess
CONFIRMED from official FAQ / reviews / retail (The Op, geekyhobbies, happypiranha, meeplemountain, BGG):
- 108 cards. Number cards now go to 13 (thirteen 13s … one 1, single 0). ✅ 13 tile added.
- 5 new action cards: Steal, Swap, Discard, Just One More, Flip Four — all TABLE-resolved → captured by ± box. ✅
- 3 special number cards:
  - Lucky 13 = keep a 2nd 13 (3rd busts). ✅ toggle
  - Unlucky 7 = discard all, keep only the 7. ✅ button
  - "0" = score 0 for the round UNLESS you Flip 7. ✅ modelled + visible note
- ÷2 (Divide) modifier halves number total. ✅ added (floor on odd).
- x2 doubles number total only. ✅ (base behaviour)
- Flip 7 → +15 self OR −15 a rival. ✅ toggle
- Score floor at 0 official; Brutal = negatives allowed. ✅ toggle
BEST-GUESS (not published anywhere public; physical cards / paywalled PDF only):
- Exact minus-card denominations → using −2,−4,−6,−8,−10 (mirrors + cards, includes the one confirmed −10).
  If real set differs, the ± box absorbs it, so scores can't be wrong.


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
