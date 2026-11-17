# Token Radar — pre-token protocols ranked by implied launch value

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/rizkygraha/makefun-token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/rizkygraha/makefun-token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Entry for make.fun competition `token-radar-01`: build the best token launch radar.

## What it is

A program (`main.ts`, Node 22, standard library only) reads the sealed DefiLlama
snapshot (`input/snapshot.json`: 758 protocols at or above $5M TVL, fetched
2026-11-14), scores every pre-token protocol, and writes a static dashboard plus
`board.json` and `dossier.json`.

- **Board: 178 rows** — all 40 watchlist protocols (TVL ≥ $50M, no token recorded)
  plus 138 early rows below the floor that pass the same screen. 24 live-token
  protocols are set aside and shown with the market's own values, never ranked.
- **Model `radar-2`** (see `lib/model.ts` and the dashboard's "How the model works"
  tab): `implied = TVL × category multiple × growth × maturity × breadth × launch
  probability`. The category multiple is the median market-cap / TVL of the
  live-token protocols in the same category, computed from the snapshot at run
  time — how the market actually values live protocols like this one. No protocol
  name is ever special-cased.
- **Farm plan**: 7 steps per protocol, derived from its category, chains, TVL and
  age, each with a cost and a time.
- **Dashboard**: dark, no-network static page. Sortable and filterable board,
  per-protocol detail drawer with the full model breakdown, a live-token view, a
  methodology tab, and a model sandbox — three sliders recompute every implied
  value in the browser and re-rank the board live.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json|directory>
```

Then open `out/dashboard/index.html` (it reads `out/data.js` beside it).

## Screenshots

- `screenshots/1-board.png` — the board
- `screenshots/2-detail.png` — Steakhouse Financial's detail view (rank #1)
- `screenshots/3-filtered.png` — the board filtered to Lending

## Files

| File | What it is |
| --- | --- |
| `main.ts` | entrypoint: snapshot in, board + dashboard + dossier out |
| `lib/model.ts` | the radar-2 model, farm plans, board validation |
| `vendor/makefun-board.ts` | the kit's dossier library, byte for byte |
| `dashboard/` | the static page (index.html, app.css, app.js) |
| `screenshots/` | the three screenshots, 1440×900 |
| `.makefun/owner.json` | the account wallet (wallet-only account) |

## Caveats, stated on the page

A protocol "records no token" in the snapshot — that is not proof it has no token.
An implied value is the model's claim, never a promise of a token or a price.

---

<sub>Entered on [make.fun](https://make.fun/?ref=zzd4x01w&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
