# Daily Trading Levels v1.0.0

Source: `daily_trading_levels.pine`

## What’s included

### Previous Day
- **PDH / PDL** — prior RTH high / low (default on)
- **PDC** — prior RTH close (default off)

### Premarket
- **PMH / PML** — high / low of the configurable premarket session (default `0400-0930` ET)

### Opening Range (from 09:30 ET)
- **5m** 09:30–09:35 (default on)
- **15m** 09:30–09:45 (default off)
- **30m** 09:30–10:00 (default off)
- **1H** 09:30–10:30 (default off)

### Intraday High / Low
- Updates continuously during **RTH only** or **Premarket + RTH**

### Previous Week / Previous Month
- **PWH / PWL** — prior week RTH high / low (default on)
- **PMoH / PMoL** — prior month RTH high / low (default on)
- Both are short right-edge marks (default 20 bars) with a label, not lines back to the source candle

### Gap
- Dotted-border fill between **yesterday’s RTH close** and **today’s RTH open**, 09:30–16:00 ET only
- Label: Gap Up / Gap Down + size

### VWAP
- Anchor: session including premarket (default) or RTH open
- Optional ±1σ / ±2σ bands (fixed color; recolor in the Style tab)

### EMAs
Eight slots (defaults: 9 green, 20 orange, 50 yellow on; 100, 200, 8, 13, 34 off). Each: On, length, color, width.

## Drawing model

- **Daily levels and gap** use `plot()` with `plot.style_linebr`, so they sit on the bars like the EMAs and VWAP and move with the chart. Values are `na` outside the **Daily levels window** (default 04:00–16:00 ET), so nothing draws overnight.
- **Show daily levels on**: `Last day only` (default) limits daily levels and the gap to the chart’s most recent trading day (ET date of the last bar). `All days` draws each day’s own levels.
- **Weekly / monthly** levels use `line.new` anchored to `bar_index`, from `last bar − N` to the last bar (N = *Weekly / monthly mark length*, default 20). They pan and zoom with the chart and add zero plot counts.
- Labels are single pills on the last bar, gated by the day so they remain after 4 PM.

## Settings pattern

For each level: **Show** toggle + **color** + **style** (Solid / Dashed / Dotted) + **width** (1–4, default 2). High and low of the same level share the high’s color. Global label toggle and size.

## Plot budget (RE10140)

Pine caps a script at 64 plot counts; a `plot()` with a color input counts 2, a `fill()` counts 1 only when its color is a series, and `line.new` / `label.new` count 0. This build uses **60**. If you add a level or EMA with a color input, remove something else or use a constant color.

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trading-levels/scripts/v1/daily_trading_levels.pine
node src/cli/index.js pine compile
```
