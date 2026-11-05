# MNQ 5-Minute ORB v1

Opening-range breakout strategy for MNQ on a **5-minute chart**.

## Rules

1. Build the opening range from the first New York regular-session candle, 9:30–9:35 ET.
2. **After that candle closes** (orders arm from the 09:35–09:40 bar onward):
   - Place a long stop one tick above the opening-range high.
   - Place a short stop one tick below the opening-range low.
   - The first filled order cancels the opposite order.
3. Default position and risk:
   - **10 contracts** (minimum allowed)
   - Stop loss: **50 MNQ index points**
   - When price touches **+50 points**, move the stop to the average entry price (breakeven)
4. Default behavior allows one trade per day (configurable up to 20) and closes any open position at 4:00 PM ET.

For MNQ, 50 index points equals 200 ticks and approximately **$100 per contract** before costs. A 100-point target is approximately **$200 per contract** before costs.

## Optional entry filters

Both filter groups are independently toggleable and enabled by default.

### RTH VWAP

- Long breakout price must be above the RTH-anchored VWAP.
- Short breakout price must be below the RTH-anchored VWAP.

The VWAP resets at 9:30 ET and only includes regular-session bars. It does not include the overnight futures session.

### EMA 9 / 21 / 50

- EMA 9, EMA 21, and EMA 50 each have an independent filter toggle.
- For every enabled EMA, long breakout price must be above it and short breakout price must be below it.
- Disable all three EMA filters to remove EMA confirmation entirely.

This tests price against the enabled averages; it does not require the EMAs themselves to be stacked in order.

## Multiple profit targets

Choose one, two, or three targets. Defaults for 10 contracts:

- **TP1:** +50 points, 4 contracts
- **TP2:** +100 points, 3 contracts
- **TP3:** +150 points, remaining 3 contracts

With two targets, TP1 uses the configured TP1 quantity and TP2 receives all remaining contracts. With one target, TP1 closes the full position. The script always reserves at least one contract for each enabled later target.

Target distances are forced into ascending order internally by at least one tick if the configured values overlap.

## Breakeven stop

**Move stop to breakeven** is enabled by default. The trigger defaults to 50 points and is configurable.

- Long: arm breakeven when the bar high touches entry + trigger.
- Short: arm breakeven when the bar low touches entry − trigger.
- Once armed, the stop stays at the average entry price until the trade closes.

On historical bars, Pine can only react using the available intrabar simulation. Enable Bar Magnifier for more realistic sequencing when the breakeven trigger and another exit are touched within the same 5-minute bar.

**Note:** When a stop (or BE stop) fills through a bracket exit, TradingView may still label the fill `Long TP1` / `Long TP2`. Use price and PnL to tell stop vs target.

## TP2 trailing rule

**After TP2, move remaining stop to TP1** is enabled by default when three targets are used:

- Long: after the TP2 allocation fills, move the TP3 stop to entry + TP1 points.
- Short: after the TP2 allocation fills, move the TP3 stop to entry − TP1 points.

Disable the option to keep the remaining TP3 stop at the normal stop/breakeven level.

## Backtest notes

- Use an **MNQ continuous or dated futures contract** on a **5-minute chart**.
- Enable TradingView’s **Bar Magnifier** for more realistic intrabar stop/target sequencing.
- Commission is initialized to `$0.62` per contract per order and slippage to one tick. Adjust these in Strategy Properties to match your broker and plan.
- TradingView historical fills are simulated. If both stop and target are touched within one bar, results depend on available lower-timeframe data and broker-emulator assumptions.
- Entry stops are submitted only **after** the 9:30–9:35 candle closes, so that candle cannot trigger a trade.
- See [`BACKTEST_ANALYSIS.md`](BACKTEST_ANALYSIS.md) for issues found in the 2026-07-18 CSV export and the v1.1.0 fix.

## Files

- `mnq_orb.pine` — Pine Script v6 strategy
- `BACKTEST_ANALYSIS.md` — review of exported list-of-trades CSV
