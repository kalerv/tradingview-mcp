# MNQ Level Break and Retest v1

`mnq_level_retest.pine` is a Pine Script v6 strategy for MNQ level breakouts, retests, and next-candle stop entries.

## Chart requirements

- Run it on a **1-minute chart with extended-hours data enabled**. Premarket levels cannot be built from an RTH-only chart.
- All sessions and daily accounting use `America/New_York`.
- The script displays a warning and disables new trading on any timeframe other than one minute.
- No `request.security`, lookahead, or future data is used.

## Levels

Each of the six levels has its own independent enable toggle and plot toggle.

1. **Premarket High / Low (PMH/PML):** accumulated from 04:00 through the 09:29 bar on weekdays. Collection ends and the values lock at 09:30 ET.
2. **Previous Day High / Low (PDH/PDL):** the prior New York RTH session's 09:30–16:00 high and low. The current RTH range is accumulated intraday and transferred to PDH/PDL at the next RTH open. This intentionally avoids a daily `request.security` call and lookahead.
3. **First 5-Minute High / Low (5mH/5mL):** accumulated from the 09:30, 09:31, 09:32, 09:33, and 09:34 one-minute bars. It becomes eligible only on the 09:35 bar and later, after the 09:34 bar has closed.

PMH, PDH, and 5mH are long-break candidates. PML, PDL, and 5mL are short-break candidates.

## Breakout and level selection

- New setups and entries are allowed only during the configurable entry session, default **09:30–11:00 ET**.
- A long breakout is close-confirmed when a one-minute bar closes at or above an enabled upper level plus the breakout buffer (default 10 points), while the prior close was below that exact threshold.
- A short breakout is the mirror: the bar closes at or below an enabled lower level minus the buffer, while the prior close was above that threshold.
- If several upper levels qualify on one bar, the strategy selects the **highest** qualifying level. If several lower levels qualify, it selects the **lowest**.
- If long and short candidates somehow qualify on the same bar, the strategy skips that bar.
- Only one setup can be active at a time. The active level and its short name are stored.
- Before entry, a long setup is invalidated by a bar close below its active level; a short setup is invalidated by a close above it.

## Retest modes

The retest candle must be after the breakout candle; the breakout candle is never its own retest.

### Standard

- Long: the candle low touches or crosses the level, does not penetrate more than the configurable 12 points below it, and closes above the level.
- Short: the candle high touches or crosses the level, does not penetrate more than 12 points above it, and closes below the level.
- A Standard retest may occur any time after the breakout and before 11:00, unless the setup is invalidated.

### Displacement

- Price must first reach the configurable displacement, default 20 points beyond the active level.
- A qualifying retest must then occur during **bars 1 through 6 after the breakout** by default. The breakout bar is bar 0.
- To avoid assuming an unknowable intrabar sequence from OHLC data, displacement must have been observed on an earlier bar; a single candle cannot establish displacement and subsequently retest.
- If no displacement-qualified retest is accepted by the end of bar 6, the Displacement path expires.

### Both

Both is the default. It accepts either:

- a Standard retest immediately, including before displacement is reached, or
- a Displacement-qualified retest within its bars 1–6 window.

After bar 6, the Displacement path expires, but the Standard path remains active until invalidation or 11:00.

## Next-candle-only entry

- At the retest candle close, the strategy submits a stop order at the retest close plus one tick for a long, or minus one tick for a short.
- The order is valid for **only the immediately following one-minute candle**.
- If that next candle does not fill the order, the order is canceled at its close and the setup resets.
- If the next candle closes through the active level while the order remains unfilled, it is invalidated and canceled.
- Entry IDs are `Level Long` and `Level Short`.
- `process_orders_on_close=false`, `calc_on_order_fills=true`, and `pyramiding=0` allow the order placed after the retest close to fill intrabar on the next bar without stacking positions.
- Pending setups and orders are canceled at/after 11:00 ET. An already-open position may continue.

## Risk and daily controls

- Fixed contracts: 10 default, minimum 1.
- Fixed stop: 50 points default.
- Fixed profit target: 100 points default.
- A full-position `strategy.exit` is maintained from `strategy.position_avg_price`.
- Maximum trades per ET day: 2 default, configurable from 1 to 10. Trades are counted on actual position entry, not setup creation.
- Trading stops after the first winning completed position of the ET day. The strategy snapshots `strategy.netprofit` on entry and compares it when the whole position returns to flat, so realized commission/slippage are included. A zero-PnL/breakeven result is not a win.
- Daily counters reset when the New York calendar date changes.
- Optional 16:00 ET position close is enabled by default.
- Backtest assumptions match the repository's MNQ scripts: $625,000 initial capital, fixed quantity, $0.62 cash commission per contract, and one tick of slippage.

## Visuals

Enabled levels use distinct `plot.style_linebr` plots. Optional minimal markers show breakout (`B`), retest (`R`), and filled entry (`E`) states, with light setup-state shading. An optional status table shows the current state, active level name, trades today, and whether a winning position has completed today.
