# token-radar-01

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Lightbeteceh/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Lightbeteceh/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token launch radar: it scores every pre-token protocol in the sealed DefiLlama snapshot (2026-11-14) with the radar-2 value model — the category multiple is the median mcap/TVL of that category's live-token protocols, shrunk toward the global median, times a damped 7-day growth term, a maturity term and a small chain-diversity term — and ranks the 226 most valuable into a sortable, filterable dashboard with concrete farm plans for each. Top pick: steakhouse-financial, implied value $1.18B. No protocol name is special-cased; the dashboard prints the computed category multiples and rechecks every row against the board, so the screen and the data are visibly the same arithmetic.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

Node 22, standard library only. The program reads the sealed snapshot, writes the ranked board to `out/board.json`, copies `dashboard/` and `screenshots/` to `out/`, and writes `out/dossier.json` for the judge.

---

<sub>Entered on [make.fun](https://make.fun/?ref=epgnnttm&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
