# Daily Trender — Changelog

## v14.1.0 — 2026-08-02

- **ORB column** — Above / Below / Inside vs opening-range high/low from 9:30 ET
- **ORB minutes** — choose one window: **5** (09:30–09:35), **15** (09:30–09:45), or **30** (09:30–10:00); header shows `ORB5` / `ORB15` / `ORB30`
- Show / Color / Filter ORB (same pattern as PrevD / PreMkt)
- ORB tracked inside existing `f_symbolBundle` (no extra `request.security`)

## v14.0.0 — 2026-07-15

- Based on **v13.0.0-rc2** (no changes to `v13-rel-cand-2`)
- **Per-ticker Enable** — inline **On** checkbox next to each ticker; uncheck to drop a slot without clearing the symbol
- **Score with PrevD / PreMkt ranges** (default **off**) — when on, sort prioritizes Above previous-day / pre-market ranges, then RS or Open %; Above+Above ranks above faster movers still Inside
- **Show table before RTH open** (default **off**) — when on, table draws in premarket using price / Mov / PrevD / PreMkt; Open % and RS are — until 9:30; sort falls back to Mov until RTH
- Hide non-bool input values from the status line / Data Window via `display = display.none` (Settings → Inputs unchanged; TV’s Style “Inputs in status line” checkbox cannot be set from Pine)

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
