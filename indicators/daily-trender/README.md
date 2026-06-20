# Daily Trender

Relative strength watchlist table vs a configurable benchmark.

## Versions

| Folder | Version | Status |
|--------|---------|--------|
| `scripts/release/` | **v8.0.0** | Frozen production release |
| `scripts/v10/` | v10 | Benchmark row + YTrend (intraday engine) |
| `scripts/v11/` | v11 | Configurable columns, ADX, RVOL |
| `scripts/v12/` | v12 | ADX/RVOL threshold color coding |
| `scripts/v13/` | **v13.0.0-rc2** | **Release candidate** — Traders Lab settings + request merge + Trend fix |

## Which to use

- **release (v8)** — stable feature set, exact final v8 behavior
- **v10** — pinned benchmark row + YTrend
- **v11** — configurable columns, ADX, RVOL, no LB
- **v12** — ADX/RVOL color tiers (20 / 25 / 2.0)
- **v13 (rc2)** — Traders Lab parity: ADX TF, filters, alerts, color toggles; RE10137 fix; Trend Long/Short/Flat
