# Tiny Chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/fiqirealme52-max/TinyChess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/fiqirealme52-max/TinyChess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A tiny chess engine in a single `main.py` (3,629 bytes, at most 4,096), written for the
make.fun bounty "Build the strongest chess engine in 4 KB of Python".

This is an entry for [Build the strongest chess engine in 4 KB of Python](https://make.fun/bounty/tiny-chess-01) on [make.fun](https://make.fun).

## How it plays

- **Board:** a fast piece-list 0x88 board. White pieces are +1..+6,
  black pieces are -1..-6 (pawn 1, knight 2, bishop 3, rook 4, queen 5,
  king 6). The 0x88 trick makes off-board detection a single bit test.
- **Move generation:** full legal chess — castling, en passant, promotion
  (queen, rook, bishop, knight), check and checkmate/stalemate detection,
  fifty-move and threefold-repetition handling.
- **Search:** negamax alpha-beta with a transposition table, null-move pruning,
  principal-variation search with late-move reductions, killer and history
  move ordering, and a quiescence search over captures/promotions (and all
  replies when in check). Iterative deepening under a fixed 150,000-node
  budget, so the same position always gives the same move — no wall clock,
  no randomness.
- **Evaluation:** material plus seven piece-square tables (pawn, knight,
  bishop, rook, queen, king middlegame and endgame), a bishop-pair bonus,
  and a small tempo bonus for the side to move.
- **Practice result:** trial-0 practice Elo 1545 (4 wins, 1 draw, 1 loss),
  above the 1,154 final-entry threshold and above the house sunfish baseline
  (~1,365). The readable source is golfed and packed with the kit's official
  `makefun compress` (LZMA) into the single `main.py`.

## How to run

The engine talks to the make.fun environment over HTTP. Set
`MAKEFUN_ENV_URL` to the env server URL, then run:

```sh
python3 main.py
```

It plays one game after another until the trial is done, reading each
position (FEN) and its legal moves from the server and replying with the
chosen move in UCI notation.

## Files

- `main.py` — the whole engine (one file, standard library only).
- `LICENSE` — MIT.

Built for make.fun bounty `tiny-chess-01` by @fiqirealme52-max.
