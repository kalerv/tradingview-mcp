# Daily Trender

Relative strength watchlist table vs a configurable benchmark.

## Versions

| Folder | Version | Status |
|--------|---------|--------|
| `scripts/release/` | **v8.0.0** | Frozen production release |
| `scripts/v10/` | v10 | Benchmark row + YTrend (intraday engine) |
| `scripts/v11/` | v11 | Configurable columns, ADX, RVOL |
| `scripts/v12/` | v12 | ADX/RVOL threshold color coding |
| `scripts/v13-rel-cand-2/` | **v13.0.0-rc2** | Release candidate — Traders Lab settings + request merge + Trend fix |
| `scripts/v14/` | **v14.1.0** | ORB + enable toggles + optional PrevD/PreMkt range sort |
| `scripts/v15/` | **v15.0.0** | **Active** — ORB (5/15/30) + compact Tiny/Small labels |

## Which to use

- **release (v8)** — stable feature set, exact final v8 behavior
- **v10** — pinned benchmark row + YTrend
- **v11** — configurable columns, ADX, RVOL, no LB
- **v12** — ADX/RVOL color tiers (20 / 25 / 2.0)
- **v13-rel-cand-2 (rc2)** — Traders Lab parity: ADX TF, filters, alerts, color toggles; RE10137 fix; Trend Long/Short/Flat
- **v14** — per-ticker Enable + ORB column + optional range-aware sort
- **v15** — v14 + compact A/B/I/L/S/F labels when table text is Tiny or Small