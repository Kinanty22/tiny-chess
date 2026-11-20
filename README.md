# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Kinanty22/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Kinanty22/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
<sub>Entered on [make.fun](https://make.fun/?ref=mjp730py&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>

A chess engine in **4,090 bytes of Python** (`main.py`), written from scratch for the make.fun `tiny-chess-01` competition ("Build the strongest chess engine in 4 KB of Python").

## How it plays

- **Board:** 0x88 representation, full legal move generation (castling, en passant, promotion, checkmate/stalemate, insufficient material, threefold repetition, fifty-move rule).
- **Search:** negamax alpha-beta with a transposition table (Zobrist keys), quiescence over captures/promotions/check replies, move ordering (TT move, MVV-LVA captures, killer moves), iterative deepening by a fixed **60,000-node budget** per move — no wall clock, fully deterministic.
- **Evaluation:** material + piece-square tables + endgame king table when neither side has a queen; incremental evaluation, updated on every make/unmake.
- **Protocol:** talks to the make.fun environment over HTTP (`POST /game`, `/move`, `/resign` at `$MAKEFUN_ENV_URL`); the env's `legal_moves` are used as an authoritative filter at the root.

## Files

- `main.py` — the entrypoint (4,052 bytes, LZMA-compressed by the kit's `compress`).
- `source.py` — the readable source it was compressed from (not committed).
- `test_perft.py`, `test_eval.py` — move-generation and evaluation tests (not committed).

## Tests

Perft: startpos 20/400/8902/197281; Kiwipete 48/2039/97862; en-passant pin 14/191/2812/43238; promotion 24/496/9483 — all match published values. Zobrist keys verified incremental == recomputed. Move generation, eval, and the env replay were verified against the kit's practice environment (legal-move sets match the env's at every checked position).

Practice trials vs the kit's house gauntlet (6 games each): trial-0 Elo 997 (1-1-4), trial-1 Elo 1099 (2-0-4), trial-2 Elo 708 (0-1-5). Per-move thinking (trial-2, 322 moves): mean 3.5 s, max 8.0 s — inside the 10 s limit. An earlier build with the bishop-pair bonus scored Elo 1451 on trial-0 (4-0-2) but did not fit the 4,096-byte cap, so the bonus was dropped. Honest read: around 900–1100 Elo on practice, near or below the 1,154 floor — a prize is a stretch, but the entry is correct and inside every size cap.

MIT licensed. Built by Muse for [@kinanty22](https://github.com/Kinanty22).
