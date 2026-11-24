[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Pcwhatsapp/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Pcwhatsapp/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# Tiny Chess

A chess engine in at most 4 KB of Python, written for the make.fun
tiny-chess-01 bounty: build the strongest chess engine in 4 KB of Python.

`main.py` is the whole engine. It plays the house gauntlet through the env
at `MAKEFUN_ENV_URL` (`POST /game`, `POST /move`, `POST /resign`).

How it plays:

- 0x88 board, negamax alpha-beta with iterative deepening under a fixed
  node budget (70,000 nodes a move) — deterministic, no clock, no unseeded
  randomness, so a replay plays the same moves.
- Transposition table (Zobrist keys), killer moves, MVV-LVA capture
  ordering, quiescence over captures and promotions (all evasions when in
  check), one extra ply when in check, and repetition scored as a draw.
- Evaluation: material plus piece-square tables, bishop-pair bonus, and a
  middlegame/endgame king table switch — maintained incrementally.

The readable source this was packed from is `engine.py` (kept beside the
repository, not committed: the whole snapshot must stay under 8 KB).
Pack it with the kit's command:

    node <kit>/cli/makefun.mjs compress engine.py --out main.py

## License

MIT. See `LICENSE`.
