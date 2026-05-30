# Flip 7 Scorer

A quick, mobile-friendly scorekeeper for the card game **Flip 7**.

- Single self-contained `index.html` — no build step, no backend, no dependencies.
- Tap a player to enter the number cards they kept, plus modifiers (+2…+10, ×2).
- Auto-calculates round scores, flags the **Flip 7 (+15)** bonus at 7 numbers, handles busts.
- First to **200** wins.
- Scores save to `localStorage` (per device/browser) — close and reopen, your game is still there.

## Scoring rules built in
- Sum of unique number cards → **×2** doubles that sum → then flat **+modifiers** are added → **+15** if 7 numbers.
- Bust = 0 for the round.

## Develop / run locally
Just open `index.html` in a browser. That's it.

## Deploy
Static site on Vercel — push to `main` and it deploys automatically.
