# Daily Trender — Release (v8.0.0)

**Frozen production release.** Do not edit except for critical hotfixes — new work goes in `v10/`.

## Features

- Benchmark presets + 18 ticker inputs
- Dark/Light theme, compact RS/Trend table
- Intraday session tracking (PDH/PDL, PMH/PML, 5m H/L)
- Configurable level price columns
- Core columns: Sym · Mov · Open · {benchmark} · RS · LB · PrevD · PreMkt · Trend

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/release/daily_trender.pine
node src/cli/index.js ui panel pine-editor open
node src/cli/index.js pine compile
```

## Note

Runs `request.security()` on every bar — may hit memory limits with 16+ tickers on 1m charts. Use `v10/` for the memory-optimized build.
