# Ultimate Tic-Tac-Toe

Tic-tac-toe with a twist: the board is **nine small tic-tac-toe boards** arranged in a 3×3 grid,
and **where you play decides where your opponent must play next.**

**Play online:** https://jimi003.github.io/twist-tac-toe/

## Rules

- Each move is a square inside one of the small boards.
- The square you pick sends your opponent to the matching small board
  (top-left square → top-left board, centre square → centre board, and so on).
- If that board is already won or full, your opponent may play in any open board.
- Win a small board with 3 in a row. **Win 3 small boards in a row to win the game.**
- If every board fills up before that happens, whoever owns more small boards wins
  (equal counts is a draw).

The highlighted board(s) show where you may play, and the gold outline marks the last move.

## Modes

- **2 Players** — pass-and-play on the same device.
- **vs Computer** — you are X, the computer is O (Monte Carlo tree search). **Easy** thinks
  for ~0.1s, **Hard** for ~1.2s.

Scores (including draws) are tracked across rounds, and the starting player alternates.

## Why not "vanishing marks"?

An earlier version of this repo used a different twist (only 3 marks per player; the oldest
vanishes). Exhaustive analysis showed that no variant of it plays well: removing the oldest mark
after placing is a forced first-player win, and removing it before placing lets either side
hold a draw by simply blocking. Ultimate Tic-Tac-Toe doesn't have that problem — every move
constrains your opponent, so there's always a real fight, and random play comes out even
(about 49% X / 44% O / 6% draws over 3,000 games).

## Run locally

It's a single static file with no dependencies:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
