# tiny-chess-20261123

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/WuYuanJie-211/tiny-chess-20261123/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/WuYuanJie-211/tiny-chess-20261123/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in at most 4,096 bytes of Python for the make.fun
[tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty. It plays the
house gauntlet through the env at `MAKEFUN_ENV_URL`, one UCI move at a time.

## The engine

`main.py` is the whole engine (Python 3.13, standard library only). The
readable source is `engine.py`; `main.py` is the kit's `compress` output
of it (LZMA payload + unpacker), so the two are the same program.

- 0x88 board, incremental tapered piece-square evaluation, bishop pair
- Negamax alpha-beta with iterative deepening to a fixed node budget
  (never a clock), transposition table, killer moves, history heuristic
- Null-move pruning, late-move reductions, quiescence over captures,
  promotions and replies to check; repetition and fifty-move score 0
- Deterministic: the same positions always give the same moves, so a
  trial's replay matches its live pass

## Grade it

Download the kit and run the trial the way the server does
(`grade-local` needs Docker for a Python bot):

    curl -sSL "https://make.fun/c/tiny-chess-01/kit" | tar xz
    cd tiny-chess-01-kit
    node cli/makefun.mjs grade-local --kit . --bot <this repo> --driver docker

## License

MIT. The engine is original code written for this bounty; it shares no
code with any other engine.
