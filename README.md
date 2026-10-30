# Twist-Tac-Toe

Tic-tac-toe with a twist: **each player can only have 3 marks on the board.**
Place a 4th and your oldest mark vanishes, so games never end in a draw.

**Play online:** https://jimi003.github.io/twist-tac-toe/

## Rules

- X and O take turns placing marks on a 3×3 grid.
- Get 3 in a row (horizontal, vertical or diagonal) to win the round.
- When you place a 4th mark, your oldest one is removed.
- The faded, pulsing mark is the one that will vanish on your next move.
  Your opponent's oldest mark is dimmed as a hint too.

## Modes

- **2 Players** — pass-and-play on the same device.
- **vs Computer** — you are X, the computer is O (depth-limited minimax).

Scores are tracked across rounds, and the starting player alternates.

## Run locally

It's a single static file with no dependencies:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
