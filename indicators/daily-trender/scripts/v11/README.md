# Daily Trender v11

Based on **v10** with configurable columns, ADX, RVOL, and LB removed.

## What's new

| Change | Detail |
|--------|--------|
| **ADX** | `ta.dmi()` on chart TF — configurable length/smoothing |
| **RVOL** | Current bar volume / SMA(volume, N) — shown as e.g. `1.5x` |
| **LB removed** | Lookback % column dropped |
| **All columns toggleable** | Settings under **Table Columns** and **Level Columns** |
| **Conditional fetch** | YTrend daily call only if YTrend shown; ADX/RVOL only if either shown |

## Column toggles (Table Columns)

- Pinned benchmark row
- Mov, Open, Benchmark %, RS, PrevD, PreMkt, Trend, YTrend, ADX, RVOL

**Sym** is always shown.

## Architecture

Same as v10: intraday `f_symbolSessionData()` every bar; YTrend once per calendar day.

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/v11/daily_trender.pine
node src/cli/index.js pine compile
```
