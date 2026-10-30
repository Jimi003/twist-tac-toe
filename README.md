# Twist-Tac-Toe

Tic-tac-toe with a twist: **each player can only have 3 marks on the board.**
Before you place a 4th, your oldest mark vanishes.

**Play online:** https://jimi003.github.io/twist-tac-toe/

## Rules

- X and O take turns placing marks on a 3×3 grid.
- Get 3 in a row (horizontal, vertical or diagonal) to win the round.
- At 3 marks, your oldest one vanishes as you place your next — and you may place
  right where it was, which is how you hold a block.
- The faded, pulsing mark is the one that will vanish on your next move.
  Your opponent's oldest mark is dimmed as a hint too.
- If the same position occurs 3 times, the round is a draw.

## Why the vanish happens *before* placing

If the oldest mark is removed *after* you place (and its cell can't be reused), the
first player wins by force by opening on an edge — the second player can't defend.
An exhaustive search of both versions confirmed this. With the current rule, best play
from both sides is a draw, so a defender can always hold, and wins come from mistakes.

## Modes

- **2 Players** — pass-and-play on the same device.
- **vs Computer** — you are X, the computer is O (depth-limited negamax; it never
  blunders into a lost position, but it punishes yours). The starting player
  alternates each round.

## Run locally

It's a single static file with no dependencies:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
