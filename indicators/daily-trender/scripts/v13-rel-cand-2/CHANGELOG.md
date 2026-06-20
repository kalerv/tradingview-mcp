# Daily Trender — Changelog

## v13.0.0-rc2 — 2026-06-20

- Fix Pine **RE10137** (40 unique `request.*()` limit) by bundling session, ADX, RVOL, and YTrend into one security call per symbol
- YTrend derived inside bundle (no extra daily security per symbol)
- Optional second ADX call only when ADX timeframe ≠ chart timeframe
- **Trend column**: Long / Short / Flat text labels with 3/3 strong and 2/3 developing alignment scoring
- Default `maxSymbols` reduced to 10 for request headroom

## v13.0.0-rc1 — 2026-06-19

- Traders Lab parity settings: ADX / Previous Day / Pre Market / RVOL groups
- Color toggles per column, row filters, ADX alerts, ADX timeframe selector
- Based on v12 ADX/RVOL threshold color coding
