# TradingView publication — Stocks Levels + EMA/VWAP v1

Source: `indicators/stocks-levels/scripts/v1/stocks_levels.pine` (v1.0.0).

TradingView house rules: the description must explain what the script does and how to use it, in plain language, with no external links or promotional text. The sections below are written to pass review as-is. Publish as **Invite-only** or **Protected** if you want the source hidden; **Open** shows the code.

---

## Title

```
Stocks Levels + EMA/VWAP — PDH/PDL, PMH/PML, ORB, Weekly/Monthly, Gap, A+ Checklist
```

Short alternative:

```
Stocks Levels + EMA/VWAP
```

---

## Description — paste into "Description"

```
Intraday key-levels overlay for stocks and ETFs. It plots the levels that most day traders watch, labels them next to the latest bar, draws the overnight gap, and summarizes where price sits relative to each level in an A+ Trade Checklist table. Session VWAP and up to 8 EMAs are included so one indicator covers the whole setup.

WHAT IT DRAWS
• Pre-market high / low (04:00–09:30 ET by default)
• Previous day high / low / open / close
• Current day open, and live current day high / low (RTH only, or premarket + RTH)
• Previous week high / low, current week high / low
• Previous month high / low
• Opening range: 1st candle (09:30–09:31), 5 min (09:30–09:35), 15 min (09:30–09:45) high / low
• After-hours high / low from the prior session (16:00–20:00 ET)
• Daily gap box from the prior regular-session close to today's open (09:30–16:00)
• Optional vertical "news time" line at a chosen hour and minute
• Session VWAP (including premarket, or anchored to the 09:30 open)
• Up to 8 EMAs with individual length, color, and width

Every level has its own show / hide, color, thickness, and line style (solid, dashed, dotted). Levels are drawn as plots, so they scroll and zoom with price like a moving average.

SHOW LEVELS ON: LAST DAY OR ALL DAYS
"Last Day" (default) draws levels, gap, and news line only for the most recent trading day, so scrolling back shows clean candles. "All Days" draws each day's own levels. Levels start at the window open (04:00 ET by default). On the latest day they continue through after-hours to the current bar so they always reach their labels; on earlier days they stop at the window close.

LABELS
Each level has a label next to the latest bar: on / off, custom text, show the price or not, text size, text color, transparent background, and an offset in bars from the last bar (10 for daily levels, 20 for weekly and monthly). A short connector in the level's color joins the last bar to the label.

PRICE AXIS
Per level, choose whether its value is shown on the price scale.

A+ TRADE CHECKLIST
A table (position, colors, and text size are configurable) with one row per selected item. Range rows (Prev Day, Pre-market, Prev Week, Current Week, Prev Month, 1st Candle, 5 min, 15 min) read Above, Inside, or Below the range. Single-level rows read Above or Below. The three words are editable. Additional rows:
• Index Trend — QQQ or SPY versus its own previous-day range (Above / Inside / Below)
• VWAP — price above or below VWAP
• Moving Average — type (EMA, SMA, WMA, VWMA, HMA), length, and timeframe
• ADX — ADX above your threshold on a chosen timeframe (Trending / Weak, with the value)
• RVOL — volume divided by its average over N bars versus your threshold (High / Low, with the value)

ALERTS
The script calls alert() when the close crosses any shown level. To receive them, create an alert on this indicator and choose the condition "Any alert() function call". The optional "No alert period" mutes alerts inside a session window (default 09:30–09:35).

HOW TO USE
1. Add to an intraday chart (1 to 15 minutes works best). Turn on extended hours in chart settings so premarket and after-hours levels have data.
2. Open Settings → Inputs. Turn levels on or off in "Price Level"; set labels in "Label"; pick checklist rows in "A+ Trade Checklist Levels".
3. Leave "Show Levels on" at Last Day for a clean chart, or switch to All Days to review how price reacted to levels on past sessions.
4. Treat levels as reference points for breakouts, retests, and reversals, and use the checklist to see at a glance whether price is above or below the areas you care about. This is a tool for context, not a signal generator.

NOTES
• All session times use the exchange timezone input (default America/New_York).
• Previous day, week, and month values are built from regular-session bars (09:30–16:00 ET).
• Pine limits a script to 64 plot counts; this indicator uses all of them, which is why weekly and monthly levels share the same drawing method as daily ones.
• Works on any symbol with intraday data; it is designed for US stocks and ETFs.
```

---

## Release notes — paste into "Describe the changes" (first publish)

```
v1.0.0 — initial release.
Levels: PM H/L, Prev day H/L/O/C, Current day open and live H/L, Prev/Current week H/L, Prev month H/L, 1st candle / 5 min / 15 min H/L, After-hours H/L. Daily gap box, news time line, per-level labels with offsets, price-axis toggles, level-cross alerts with a no-alert window, A+ Trade Checklist table (Index trend, ranges, VWAP, MA, ADX, RVOL), session VWAP, and up to 8 EMAs.
```

---

## Tags (TradingView allows a few)

```
levels, premarket, previous day high, ORB, opening range, gap, VWAP, EMA, day trading, support and resistance
```

---

## Chart for the publication

TradingView uses the chart that is open when you click Publish. Suggested setup:
- QQQ or SPY, 1 or 5 minute, extended hours on, showing a full day from 04:00 through after-hours.
- Defaults on (PM, Prev day, Prev week, 1st candle, 5 min, current day H/L, gap, checklist table).
- Keep other indicators off so the labels and table are readable.
