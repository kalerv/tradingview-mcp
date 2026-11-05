# Stocks Levels + EMA/VWAP

Feature-for-feature rebuild of the paid "TL_StocksLevels" indicator (reference screenshots in
`../daily-trading-levels/scripts/v1/refrence_indicator_images/`), plus session VWAP and up to 8 EMAs.

## Versions

| Folder | Version | Status |
|--------|---------|--------|
| `scripts/v1/` | **v1.0.0** | **Active** (published Line-only build) |
| `scripts/v2/` | **v2.0.0-zones** | **Sandbox** — same as v1 plus a Zone Lab for testing band styles |

## Settings groups (match the reference, top to bottom)

### Price Level
- **Show Levels on**: `Last Day` (default) or `All Days`
- Timezone (`America/New_York`), **Levels window** (`0400-1600`), Pre-market session (`0400-0930`), After-hours session (`1600-2000`)
- 23 levels, each with **show / color / thickness / style** (solid, dashed, dotted):

| Level | Default | Source |
|-------|---------|--------|
| Pre-market high / low | on, blue, 2 | high/low of the premarket session today |
| Prev day high / low | on, gold, 2 | prior day RTH 09:30–16:00 |
| Prev day open / close | off, 1 | prior day RTH open / close |
| Current day open | off, white, 1 | today's 09:30 open |
| Current day high / low | on, green dashed, 2 | live intraday high / low; **Current day H/L session** = RTH only (default) or Premarket + RTH |
| Prev week high / low | on, green, 2 | prior week RTH |
| Current week high / low | off, pink, 1 | running week RTH |
| Prev month high / low | off, green, 2 | prior month RTH |
| 1st Candle high / low | on, purple, 2 | 09:30–09:31 |
| 5 min Candles high / low | on, purple, 2 | 09:30–09:35 |
| 15 min Candles high / low | off, purple, 2 | 09:30–09:45 |
| After-hour high / low | off, violet, 1 | prior day's 16:00–20:00 session |

### Price Axis
One checkbox per level: show its value on the price scale (plot `display.price_scale`). Default on for PM H/L, Prev day H/L, Prev week H/L.

### Label
Per level: **on**, **Display price after label text**, **Text**, **Size**, text color (default black), **Transparent** background, and **offset from last bar** (10 for daily levels, 20 for weekly / monthly). Labels sit to the right of the latest bar and are joined to it by a short connector in the level's color.

### No Alert Period
- **Level cross alerts** (on): `alert()` fires when the close crosses any shown level. Create the TradingView alert with condition **"Any alert() function call"**.
- **No alert period** (off, `0930-0935`): mutes alerts inside the window.

### News Time Line
Vertical line at **Hour : Minutes** ET (default 10:00) on each shown day. Color, thickness, style.

### Daily Gap
Box from prior RTH close to today's RTH open, 09:30 through 16:00. Border thickness (3), border color, fill color, border style (dashed).

### A+ Trade Checklist
Table with position, text / background / frame / border colors, up / down colors, text size, **Market measuring Index** (QQQ or SPY), and the three status words (Above / Inside / Below).

### A+ Trade Checklist Levels
Rows to include. Range rows (Prev Day, Pre-market, Prev Week, Current Week, Prev Month, 1st Candle, 5 min, 15 min) show Above / Inside / Below; single-level rows show Above / Below. Also:
- **Index Trend**: index close vs. the index's own previous-day RTH range (Above / Inside / Below)
- **VWAP**: price vs. VWAP
- **Moving Average**: type (EMA / SMA / WMA / VWMA / HMA), length, timeframe
- **ADX**: ADX > threshold on a chosen timeframe → Trending / Weak, with value
- **RVOL**: volume / SMA(volume, N) ≥ threshold → High / Low, with value

### VWAP / EMAs (additions)
Session VWAP (incl. premarket, or RTH-anchored), red, width 2. Eight EMA slots (9 green, 20 orange, 50 yellow on by default).

## Drawing model

- Levels, VWAP, EMAs are `plot()` series on the bars, so they pan and zoom with price. Daily levels start at the levels window open (default 04:00 ET). On the chart's latest day they continue through after-hours to the current bar, so the lines reach the labels; on earlier days (All Days mode) they stop at the window close. In `Last Day` mode nothing is drawn on earlier days.
- Labels, connectors, gap box, and news line are `line` / `label` / `box` drawings anchored to `bar_index`.
- The table and `alert()` use no plot counts.

## Plot budget (RE10140)

64 plot counts max. A `plot()` with a color input counts 2. This script: 23 levels + VWAP + 8 EMAs = 32 plots × 2 = **64** (full). To add another plotted level, drop an EMA slot or give something a constant color.
