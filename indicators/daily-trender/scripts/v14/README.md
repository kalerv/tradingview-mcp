# Daily Trender v14.1.0

Based on **v13.0.0-rc2** with ticker enable toggles, optional PrevD/PreMkt range scoring, and an ORB column.

## What’s new in v14.1

### ORB Settings

- **Show ORB** — Above / Below / Inside vs the selected opening-range high/low (same style as PrevD / PreMkt)
- **ORB minutes** — only one window at a time: **5** (09:30–09:35), **15** (09:30–09:45), **30** (09:30–10:00) ET
- Header label is `ORB5`, `ORB15`, or `ORB30`
- Optional **Filter ORB** — keep rows matching Above / Below / Inside
- Not part of Trend scoring or “Score with PrevD / PreMkt ranges”

## What’s new in v14

### Tickers — Enable (On)

Each ticker row has an **On** checkbox. Uncheck to remove that symbol from the table without clearing the field. Use with **Max symbols to fetch** to watch a small set (e.g. 5) while keeping other symbols configured.

### Score with PrevD / PreMkt ranges (Settings)

- Default **off** — sort is RS vs benchmark or Open % only (same as v13)
- When **on** — primary sort by range breakout points (PrevD Above +1, PreMkt Above +1), then secondary RS/Open %
- Example: Above+Above with RS +0.5 ranks above Inside+Inside with RS +2.0
- Does **not** change Trend column scoring; row filters (Above/Below/Inside) are unchanged

### Show table before RTH open (Settings)

- Default **off** — table appears after 9:30 ET when Open % is available (same as v13)
- When **on** — rows show in premarket if price is available; Mov / PrevD / PreMkt work; Open % and RS show — until the open; sort uses Mov (or Mov vs bench) until RTH
## Settings groups (from v13)

### ADX Settings
- Show ADX / **Color ADX** toggles
- **Time Frame to Use** — Chart, 1, 5, 15, 60, D
- **ADX Threshold** — default **25** (strong trend + alerts)
- **Alert when ADX above Threshold** + **Alert Period** (default 09:30–16:00)
- **Filter stocks with ADX (>) above** — default **20**
- ADX length / smoothing (14)

### Previous Day Settings
- Show / **Color** toggles
- **Filter Previous Day** — Above / Below / Inside

### Pre Market Settings
- Show / **Color** toggles
- **Filter Pre-Market** — Above / Below / Inside

### ORB Settings
- Show / **Color** toggles
- **ORB minutes** — 5 / 15 / 30 (one at a time)
- **Filter ORB** — Above / Below / Inside

### RVOL Settings
- Show / **Color** toggles
- **Volume Average Length** — default **14**
- **RVOL Threshold** — default **2.0** (high = green)
- RVOL low — default **1.0** (weak = red)

## ADX colors (when Color ADX on)

| ADX | Color |
|-----|-------|
| < filter min (20) | Gray — choppy |
| 20–25 | Amber — developing |
| ≥ 25 + +DI > -DI | Green ▲ |
| ≥ 25 + -DI > +DI | Red ▼ |

## Alerts

Enable **Alert when ADX above configured Threshold** and create a TradingView alert on the indicator. Fires once per bar close for each watchlist symbol with ADX ≥ threshold during the alert period.

## Request limit (RE10137)

Pine allows **40 unique `request.*()` calls** per script. v14 keeps v13’s merge: **one `request.security` per symbol** via `f_symbolBundle()`.

| Setting | Calls per symbol |
|---------|------------------|
| ADX TF = **Chart** | 1 |
| ADX TF = 1/5/15/60/D | 2 (chart bundle + ADX TF) |

**Default `maxSymbols` = 10** leaves headroom for the benchmark row (+ optional alt ADX). Reduce symbols or keep ADX on Chart if you hit the limit.

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/v14/daily_trender.pine
node src/cli/index.js pine compile
```
