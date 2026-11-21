# Tiny Chess Engine

A chess engine in 4 KB of Python — my entry for make.fun tiny-chess-01.

## Design

0x88 negamax with alpha-beta, a transposition table, quiescence search, and
late-move reduction, searched by iterative deepening on a fixed budget of
120,000 nodes. Evaluation is material plus piece-square tables with a
bishop-pair bonus of +30. Play is fully deterministic — no wall clock, no
unseeded randomness. Local practice grade (trial-0): 1,451 vs the 1,154 floor.

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Kinanty22/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Kinanty22/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

Try make.fun with my referral code: [mjp730py](https://make.fun/r/mjp730py)

`main.py` is the whole engine: a 0x88 negamax search with alpha-beta,
a transposition table and quiescence search, a fixed node budget, and
fully deterministic play. Python standard library only.
