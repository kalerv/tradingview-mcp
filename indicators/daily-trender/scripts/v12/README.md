# Daily Trender v12

Based on **v11** with Traders Lab–style ADX/RVOL threshold coloring.

## What's new

### Configurable thresholds (ADX / RVOL settings)

| Input | Default | Meaning |
|-------|---------|---------|
| ADX min trend threshold | **20** | Below = choppy / stay out |
| ADX strong trend threshold | **25** | Strong trend + DI direction |
| RVOL high | **2.0** | High participation (winning setup) |
| RVOL low | **1.0** | Low participation (fade risk) |

### ADX cell colors

| ADX | Background | Notes |
|-----|------------|-------|
| **< 20** | Gray | No trend — likely chop / stay out |
| **20–25** | Amber | Developing trend |
| **≥ 25** + **+DI > -DI** | Green | Strong bullish momentum (shows `▲`) |
| **≥ 25** + **-DI > +DI** | Red | Strong bearish momentum (shows `▼`) |

### RVOL cell colors

| RVOL | Background |
|------|------------|
| **≥ 2.0x** | Green — high interest |
| **≤ 1.0x** | Red — weak participation |
| Between | Gray |

### Setup logic (manual read)

**Favorable long context:** green RVOL (≥ 2.0) + green ADX (≥ 25, +DI leading).

**Stay out:** red/gray ADX (< 20) + red RVOL (≤ 1.0) on a big candle — likely no follow-through.

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/v12/daily_trender.pine
node src/cli/index.js pine compile
```
