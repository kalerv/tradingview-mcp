# Break and Bounce v2

Architecture revision: multi-level pool, sequencing, entry/SL/TP mode toggles.

## vs v1

| Feature | v1 | v2 |
|---------|----|----|
| Levels | PDH/PDL only | + PMH/PML, 5MH/5ML, IDH/IDL (TP only) |
| Concurrent setups | Single level | All enabled levels in parallel |
| Daily trades | Unlimited | Max 2; 2nd only after 1st loss |
| Breakout TF | Hardcoded 5m | Input (chart must match) |
| Entry | Immediate only | Immediate / Confirmation stop |
| SL | Structural pivot only | + Retest candle extreme |
| TP | Fixed 2R only | + Ceiling ladder (IDH/IDL tiers) |

## Push to TradingView

```bash
node src/cli/index.js pine set --file strategies/breakandretest/scripts/v2/break_and_bounce.pine
node src/cli/index.js ui panel pine-editor open
node src/cli/index.js pine compile
```

## Chart

Set chart timeframe to match **Breakout Timeframe** input (default 5m).

## Spec

`docs/break_and_bounce_spec_v2.md` (when added) — implementation follows v2 architecture prompt.
