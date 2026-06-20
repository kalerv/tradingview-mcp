# Daily Trender v10

Based on **release v8.0.0** with pinned benchmark row + YTrend column.

## Architecture

| Layer | When it runs | What |
|-------|----------------|------|
| **Intraday** | Every bar | `f_symbolSessionData()` on chart TF (same engine as release) |
| **YTrend** | Once per calendar day | Daily `[close[1], high[2], low[2]]` → Bull BO / Bear BO / Inside |
| **Table draw** | `islastconfirmedhistory` or `islast` | Renders from fresh intraday arrays + cached YTrend |

Intraday columns (Mov, Open, RS, LB, PrevD, PreMkt, Trend, level prices) update every bar — including replay.

YTrend is yesterday's context; it only refetches when the calendar day changes (or on first load).

## v10 extras vs release

- Pinned benchmark row (highlighted row 1)
- YTrend column (day-cache, not intraday)
- `maxSymbols` cap (default 12)

## If you hit memory limits

1. Lower **Max symbols to fetch** (try 8)
2. Use **release** for the stable 18-symbol table without YTrend / benchmark row

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/v10/daily_trender.pine
node src/cli/index.js pine compile
```
