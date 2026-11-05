# QQQ 9:31 Range Breakout

Pine Script v6 strategy. Use a **1-minute** QQQ chart.

TradingView trades shares, not option contracts. A long is the stand-in for a **5-day QQQ call** (ATM or 1 strike out of the money). A short is the stand-in for the **put**. Default size is **2 shares**.

## Setup

Wait for the **09:30–09:31 ET** candle to close. That bar’s high and low are the range.

Example: high `607.51`, low `606.85`.

## Entry

After that candle closes, on the same regular session:

- Price trades **above the high** → buy 2 QQQ shares (call).
- Price trades **below the low** → short 2 QQQ shares (put).

Only the first break fills. The other stop is canceled. No new entry that day if a position from an earlier session is still open at 9:30.

## Exit

Whichever comes first:

- **$5 in favor** of the fill price. Long from 605 sells at 610. Short from 605 covers at 600.
- **Stop loss**, only when **Use stop loss** is on. Default is **$5** against the fill. A long from 605 stops at 600. A short from 605 stops at 610. With the flag off, a losing trade is held until the day limit.
- **1 to 5 regular sessions**, set by **Days to hold** (default 5). The entry session counts as day 1. If the profit target has not hit, the position closes on the 15:59 ET bar of the selected day.

Profit, stop, and hold length are inputs (`Favorable exit ($)`, `Use stop loss`, `Stop loss ($)`, `Days to hold`).

## Chart

Times use `America/New_York`. Run it on QQQ, 1-minute, with regular-session data through 16:00 ET so the time exit has a last RTH bar.
