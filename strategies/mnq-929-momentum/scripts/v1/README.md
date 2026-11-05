# MNQ 9:29 Close Momentum

Pine Script v6 strategy for MNQ that trades the close-to-close direction of the 09:29 ET candle.

## Chart requirements

- Use a **1-minute chart**. The strategy does not trade on any other timeframe and displays a warning table.
- The chart must contain extended-hours data so that both the 09:28 and 09:29 ET bars exist.
- Times are evaluated in `America/New_York` by default.

## Entry rules

At the close of the 09:29 ET candle in the default normal mode:

- Enter long at market when the 09:29 close is greater than the immediately preceding 09:28 close.
- Enter short at market when the 09:29 close is less than the immediately preceding 09:28 close.
- Do nothing when the two closes are equal.
- Do nothing if the 09:28 close for that ET day was not captured.

The 09:29 candle's open and candle color are irrelevant. “Green” momentum means its close is above the stored 09:28 close; “red” momentum means its close is below that close.

The **Reverse signal direction** entry option is disabled by default. When enabled, a valid bullish setup enters short and a valid bearish setup enters long. Entry IDs always describe the actual position direction (`9:29 Long` or `9:29 Short`), including in reverse mode.

`process_orders_on_close=true` places the market entry on the 09:29 close. Entry IDs are `9:29 Long` and `9:29 Short`. The strategy stores the 09:28 close when that bar confirms, then compares on 09:29. It permits at most one signal/entry per ET calendar day, including order-fill recalculations.

## Filters

Every enabled filter must pass at the 09:29 close:

- EMA 9: original bullish setup above / original bearish setup below.
- EMA 21: original bullish setup above / original bearish setup below.
- EMA 50: original bullish setup above / original bearish setup below.
- Session VWAP: original bullish setup above / original bearish setup below.

Each EMA filter is independently configurable.

Filters are always evaluated against the **original close-to-close setup direction before reversal**. For example, a bullish setup must be above every enabled bullish filter; if it passes and reverse mode is enabled, the strategy then enters short. Reverse mode does not reinterpret that setup using the short/below filter conditions. This ordering supports contrarian testing without changing which momentum setups qualify.

### Session VWAP distinction

This strategy uses `ta.vwap(hlc3)`, labeled **Session VWAP**. It is the current daily/session VWAP provided by the chart's available data, including premarket data when extended hours are enabled. It is not an RTH-only VWAP: an RTH VWAP beginning at 09:30 cannot exist when the signal is evaluated at the 09:29 close.

## Risk and profit management

- Position size has a minimum of 10 contracts.
- A fixed stop-loss distance is applied from the average entry price.
- Optional breakeven management moves the stop to the average entry after the configured favorable move.
- One, two, or three profit targets can be selected.
- With two targets, TP1 uses its configured quantity and TP2 receives the remainder.
- With three targets, TP1 and TP2 use their configured quantities and TP3 receives the remainder; the script reserves at least one contract for every later target.
- Optional runner management moves TP3's stop to the TP1 price after TP2 has filled.
- An open position is closed at 16:00 ET when the session-close option is enabled.

## Visuals

The strategy can plot Session VWAP and EMA 9/21/50. A subtle background highlight marks the 09:29 signal bar: green for a valid final long, red for a valid final short, and gray when the setup is filtered out, tied, or missing. In reverse mode, the color therefore follows the actual trade direction rather than the original setup direction.
