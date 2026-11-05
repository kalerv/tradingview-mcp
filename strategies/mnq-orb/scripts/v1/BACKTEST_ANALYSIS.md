# Backtest report analysis — MNQ ORB export

## Latest export (v1.1.0 check)

Source: `~/Downloads/MNQ_ORB_CME_MINI_MNQ1!_2026-07-18_29a3f.csv`

### Verdict

**ORB arming fix is working.** Compared to the prior export:

| Check | Old (`4db36`) | New (`29a3f`) |
|-------|---------------|---------------|
| 09:35 entry legs | 3,172 | 1,440 |
| Same-bar entry+exit at 09:35 | **1,664** | **0** |
| Days with long+short both at 09:35 | **70** | **0** |
| Trade legs | 11,889 | 10,515 |

Remaining **09:35** timestamps are expected: TradingView labels the bar by **open** time, so the first post-ORB bar (09:35–09:40) shows as `09:35`. Those trades exit later (duration ≥ 1 bar), not on the same bar.

### Still settings, not script bugs

This run still looks like custom inputs (not script defaults):

- Qty mostly **5** → 10 contracts / 2 targets
- Wins cluster at **+25 / +50** → TP1/TP2 distances
- Losses cluster at **−10.25** → ~10-point stop + 1-tick slippage
- Exit names `Long TP1`/`Long TP2` on losses → stop fill still labeled with the exit id (TV quirk)

### Prior export (pre-fix)

Source: `strategies/mnq-orb/scripts/v1/MNQ_ORB_CME_MINI_MNQ1!_2026-07-18_4db36.csv`

Critical bug: stops armed on the 9:30–9:35 candle, so that bar could fill long and/or short and often stop out immediately. Fixed in v1.1.0 by requiring `bar_index > orbReadyBar` and breakout stops at high/low ± 1 tick.
