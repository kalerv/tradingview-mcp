# Stocks Levels — Zone Lab (v2)

Sandbox copy of v1. The published script stays at `scripts/v1/`. Add **this** file to the chart as a second indicator (`SLV-Z`) to try zone styles.

Source: `stocks_levels.pine`

## How to test

1. Keep v1 on the chart if you want the clean lines as a reference, or use only v2.
2. Open **Zone Lab (v2 — experiment)**.
3. Change **Zone style** first, then **Zone span** and **Zone width**.
4. Leave **Keep the midline** on so you can see the exact level inside the band.

ORB, opens/closes, and live current-day / current-week H/L stay single lines in every style.

## Zone styles

| Style | What you see |
|-------|----------------|
| **Off (lines only)** | Same as v1 |
| **Cream shelf** | One muted beige band per major level (TSLA-example look) |
| **Level-colored halo** | Band uses that level’s color at high transparency |
| **Stop-side band** | Highs grow **above** the level, lows grow **below** (where stops sit) |
| **Outline only** | Empty box, cream border, no fill |

## Zone span

| Span | Horizontal range |
|------|------------------|
| **Session window** | Same as the level line (4:00 ET → last bar on the latest day) |
| **Day start** | From the first bar of the ET calendar day |
| **Visible range** | Left of the current viewport → last bar (redraws when you pan/zoom) |

## Width

- **ATR** — `ATR(length) × multiplier × horizon` (default 0.25 × ATR)
- **Fixed $** — same dollar height on every symbol
- **Percent** — `% of current price` (default 0.08%)
- **Ticks** — `N × mintick`

Horizon multipliers: daily (PD / PM / AH) 1.0×, weekly 1.5×, monthly 2.0×.

Each Price Level row has a **Zone** checkbox (last box on the row, tooltip “Zone — solid band for this level”). Only checked levels get a band. Style / span / width in Zone Lab apply to those checked levels.

## Suggested first pass

1. Style **Cream shelf**, span **Visible range**, width **Percent 0.08** — closest to the TSLA screenshot.
2. Same settings with **Stop-side band** — check whether one-sided shelves read better.
3. Style **Level-colored halo**, span **Session window**, width **ATR 0.25** — check color-coded bands on the same span as the lines.

Tell me which combo looks right and we promote that one back into a real version.
