# Daily Trender v13.0.0-rc2

**Release candidate 2** — based on **v12** with **Traders Lab Dashboard**–style settings parity.

## RC2 fixes (vs rc1)

- **RE10137** — merged `request.security` calls via `f_symbolBundle()` (session + ADX + RVOL + YTrend in one call per symbol)
- **Trend column** — visible Long / Short / Flat labels (2-of-3 or 3-of-3 alignment scoring)
- Default `maxSymbols` = 10 for Pine 40-call request limit headroom

## Settings groups (matches Traders Lab UI)

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

Pine allows **40 unique `request.*()` calls** per script. v13 merges session, ADX, RVOL, and YTrend into **one `request.security` per symbol** via `f_symbolBundle()`.

| Setting | Calls per symbol |
|---------|------------------|
| ADX TF = **Chart** | 1 |
| ADX TF = 1/5/15/60/D | 2 (chart bundle + ADX TF) |

**Default `maxSymbols` = 10** leaves headroom for the benchmark row (+ optional alt ADX). Reduce symbols or keep ADX on Chart if you hit the limit.

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/v13/daily_trender.pine
node src/cli/index.js pine compile
```
