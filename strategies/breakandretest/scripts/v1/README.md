# Break and Bounce v1

Pine Script v6 **strategy** (not indicator) — first retest of PDH/PDL with volume quadrant resolution.

## Files

| File | Purpose |
|------|---------|
| `break_and_bounce.pine` | Source of truth for this version |
| `CHANGELOG.md` | Version history |
| `../results/v1.0.0/` | Screenshots + metrics after backtests (create when testing) |

## Push to TradingView

```bash
cp strategies/breakandretest/scripts/v1/break_and_bounce.pine scripts/current.pine
node scripts/pine_push.js
# or:
node src/cli/index.js pine set --file strategies/breakandretest/scripts/v1/break_and_bounce.pine
node src/cli/index.js pine compile
node src/cli/index.js pine errors
```

## Chart requirements

- **Timeframe:** 5 minutes (required)
- **Session:** US equities/futures with 9:30–11:30 ET window
- **Pine editor:** open before push

## Spec reference

See `strategies/breakandretest/docs/break_and_bounce_spec.md`
