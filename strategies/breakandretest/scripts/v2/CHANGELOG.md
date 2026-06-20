# Break and Bounce — v2.0.0

## v2.0.0 — 2025-06-19

Architecture revision from v1:

- **§2** Level pool: PDH/PDL + PMH/PML (stocks/ETFs) + 5MH/5ML + IDH/IDL (TP ladder only)
- **§3** Multi-level parallel state machine; first resolve wins; max 2 trades/day
- **§4–§6** Breakout/retest/volume engine unchanged, generalized per level + `close[1]` inside-level fix
- **§8** Entry mode: Immediate / Confirmation stop with cancel rules
- **§9** SL mode: Structural swing / Retest candle extreme
- **§10** TP mode: Fixed 2R / Ceiling ladder (60/30/10 default)
- **§11** breakoutTF, retestTF, entryTF inputs
- **§7** Extended debug table

Compiles clean on TradingView pine-facade.
