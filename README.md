# Tic-Tac-Toe with a twist

Two twisted tic-tac-toe games in one static site.

**Play online:** https://jimi003.github.io/twist-tac-toe/

| Game | Page | Twist |
|---|---|---|
| **Ultimate Tic-Tac-Toe** | [`index.html`](index.html) | Nine small boards; where you play decides where your opponent must play next. |
| **Duel Tic-Tac-Toe** | [`duel.html`](duel.html) | Both players pick a square *at the same time*. Pick the same one and it's rock-paper-scissors for it. |

---

## Ultimate Tic-Tac-Toe

The board is **nine small tic-tac-toe boards** arranged in a 3×3 grid, and **where you play
decides where your opponent must play next.**

### Rules

- Each move is a square inside one of the small boards.
- The square you pick sends your opponent to the matching small board
  (top-left square → top-left board, centre square → centre board, and so on).
- If that board is already won or full, your opponent may play in any open board.
- Win a small board with 3 in a row. **Win 3 small boards in a row to win the game.**
- If every board fills up before that happens, whoever owns more small boards wins
  (equal counts is a draw).

The highlighted board(s) show where you may play, and the gold outline marks the last move.

### Modes

- **2 Players** — pass-and-play on the same device.
- **vs Computer** — you are X, the computer is O (Monte Carlo tree search). **Easy** thinks
  for ~0.1s, **Hard** for ~1.2s.

Scores (including draws) are tracked across rounds, and the starting player alternates.

---

## Duel Tic-Tac-Toe

Normal 3×3 board, but nobody waits for a turn. **Every round, both players secretly pick an
empty square and a throw (rock, paper or scissors), then reveal together.**

### Rules

- **Different squares:** both marks land.
- **Same square (a clash):** the throws decide. Rock beats scissors, scissors beat paper, paper
  beats rock. The winner takes the square, the loser places nothing that round, and a tie leaves
  the square open.
- Three in a row wins. If both players complete a line in the same round, or the board fills up,
  it's a draw.

Your throw only matters if you clash, so the real game is guessing which square your opponent
wants: go for the winning square and they may block it, and a clash is a coin-flip-ish gamble
for both of you.

### Modes

- **vs Computer** — **Easy** grabs wins, usually blocks, and likes the centre and corners.
  **Hard** plays the exact game-theoretic mixed strategy for every position, so it can't be
  out-guessed (it can still lose to luck).
- **2 Players** — pass-and-play. Each player locks in their pick behind a "pass the device"
  screen, so the other player never sees it before the reveal.

### Why this twist is fair

The game is symmetric (both sides have the same options at the same time), so with best play
neither side has an edge. I solved it exactly: all 11,093 reachable positions, with a linear
program per position, and checked the shipped table and strategy solver against every one
(the computer's strategy can be exploited for at most 0.006 of a point per round). Simulated
games: Hard vs Hard comes out about 36% X / 34% O / 30% draws, and Hard beats Easy 51% to 16%
(and random play 83% to 3%).

The computer's brain is `duel-table.js`, a generated lookup table of position values.
Regenerate it with `python3 tools/gen_duel_table.py` (needs `scipy` and `numpy`).

---

## Why not "vanishing marks"?

An earlier version of this repo used a different twist (only 3 marks per player; the oldest
vanishes). Exhaustive analysis showed that no variant of it plays well: removing the oldest mark
after placing is a forced first-player win, and removing it before placing lets either side
hold a draw by simply blocking. I also solved a dozen other rule changes (rotating ring, ABBA
turn order, restricted moves, swaps, sliding rows, RPS piece-flipping, …): nearly all of them
give one side a forced win, which is why the two games above exist.

## Run locally

It's a static site with no build step and no dependencies:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```
