# Daily Trading Levels

Overlay indicator that marks key daily levels, opening ranges, the overnight/open gap, previous week / month marks, optional VWAP, and up to 8 EMAs.

## Versions

| Folder | Version | Status |
|--------|---------|--------|
| `scripts/v1/` | **v1.0.0** | **Active** |

## Levels

| Level | Meaning |
|-------|---------|
| **PWH / PWL** | Previous week RTH high / low — short mark at the latest bar |
| **PMoH / PMoL** | Previous month RTH high / low — short mark at the latest bar |
| **PDH / PDL** | Previous regular-session (RTH) high / low |
| **PDC** | Previous RTH close (optional) |
| **PMH / PML** | Premarket high / low (default 04:00–09:30 ET) |
| **1st Candle** | Opening bar 09:30–09:31 ET |
| **5mH / 5mL** | Opening range 09:30–09:35 ET |
| **15mH / 15mL** | Opening range 09:30–09:45 ET |
| **30mH / 30mL** | Opening range 09:30–10:00 ET |
| **1HH / 1HL** | Opening range 09:30–10:30 ET |
| **IDH / IDL** | Intraday high / low (updates continuously) |
| **Gap** | Box from prior RTH close → today’s RTH open (dotted border) |

## Also included

- **VWAP** — full session (incl. premarket, default) or RTH open; optional ±1 / ±2σ bands
- **EMAs** — up to **8** slots; each has On / length / color / width

Every level and overlay has show/hide, color, line style (solid / dashed / dotted), and width where applicable. High and low of the same level share one color.

## When levels show

- **Daily levels** (PD, PM, ORB, intraday) and the **gap** are `plot()` series on the bars, so they scroll and zoom with price. They draw only inside the **Daily levels window** (default **4:00 AM–4:00 PM ET**); the gap fill is 9:30 AM–4:00 PM ET.
- **Show daily levels on** — `Last day only` (default) draws them for the most recent trading day only, so scrolling back shows clean candles. `All days` draws each day’s own levels.
- **Weekly / monthly levels** are short marks (default 20 bars) ending at the latest bar with a label. They never extend back to the candle that set them. Length is configurable.
- Labels sit on the latest bar and stay visible after the window closes for that day.

## Plot budget

Pine allows 64 plot counts per script (runtime error **RE10140** otherwise). A `plot()` with a user-selectable color counts **2**; `line.new` / `label.new` count 0. This script sits at **60**: 17 daily levels, 2 gap borders, VWAP, and 8 EMAs with color inputs, plus 4 VWAP band plots with a fixed color. Recolor the bands in the **Style** tab if needed. Adding one more color-input plot costs 2.

## Chart

Works on any intraday chart. Times use `America/New_York` by default. Use extended-hours data for premaket levels.
