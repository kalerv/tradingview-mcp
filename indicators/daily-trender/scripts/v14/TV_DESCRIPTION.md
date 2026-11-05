# TradingView description updates — Daily Trender v14

Use this when updating the published indicator description on TradingView. It lists **corrections to the current text**, **new material for this release**, and a **ready-to-paste revised description**.

Source version: `indicators/daily-trender/scripts/v14/daily_trender.pine` (v14.1.0, based on v13.0.0-rc2).

---

## Corrections to the current published text

These lines in the live Overview are outdated or inaccurate — update them even if you only ship a short “What’s new” blurb.

| Current copy | Change to |
|--------------|-----------|
| “up to 18 tickers” as the practical default | Still **up to 18 slots**, but **Max symbols to fetch** defaults to **10** (Pine 40-request limit). Enable only the slots you need. |
| RVOL = “today’s cumulative session volume compared to yesterday’s volume pace” | **Correct:** RVOL = chart-timeframe **bar volume ÷ SMA(volume, length)** (default length 14). Color thresholds: high (default 2.0×), low/weak (default 1.0×). |
| Trend = “only fires when RS, PrevD, and PreMkt all agree” | **Correct:** Trend shows **Long / Short / Flat** from PrevD + PreMkt + RS alignment (**3/3** = strong, **2/3** = developing, mixed = Flat). |
| “some columns (since-open, RS) will show no value before the regular session” / table implied empty | Still true by **default**. New optional setting can show the table in premarket (see below). |
| Settings list only “ADX/DMI length” + level toggles | Expand to match Groups below (filters, ADX TF, alerts, column color toggles, sort options, ticker On, etc.). |

---

## What’s new to mention in this release

### New in v14.1

1. **ORB column** — Above / Below / Inside vs opening-range high/low from 9:30 ET. Choose **5**, **15**, or **30** minutes (only one window active). Optional Show / Color / Filter like PrevD / PreMkt. Header: `ORB5` / `ORB15` / `ORB30`.

### New in v14

1. **Per-ticker On toggle** — Each ticker has an Enable checkbox beside the symbol. Uncheck to drop a name from the table without clearing the field (e.g. monitor 5 names while keeping the other slots saved).
2. **Score with PrevD / PreMkt ranges** (Settings, default **off**) — When on, sort prioritizes tickers **Above** the prior-day and/or premarket range, then RS or Open %. A name **Above both** ranks above a faster mover still **Inside** those ranges.
3. **Show table before RTH open** (Settings, default **off**) — When on, the table draws in premarket using price / Mov / PrevD / PreMkt; Open % and RS show as — until 9:30; sort falls back to Mov until the regular open.
4. **Cleaner status line** — Non-bool input values are hidden from the status line / Data Window (`display.none`). Settings → Inputs is unchanged. (TV’s Style “Inputs in status line” checkbox still cannot be set from Pine.)

### From v13 (likely missing from the current Overview — include if not already published)

- Toggleable table columns (Mov, Open, Bench %, RS, PrevD, PreMkt, ORB, Trend, YTrend, ADX, RVOL, levels)
- Pinned benchmark row (optional)
- Sort by **RS vs benchmark** or **Open % since RTH open**
- **Previous Day / Pre-Market / ORB** show + color + **row filters** (Above / Below / Inside)
- **ADX** timeframe, threshold (25), color tiers, filter (min 20), optional ADX alerts in a session window
- **RVOL** show/color + high/low thresholds
- Request bundling for Pine’s 40-call limit; default max symbols = 10

---

## TradingView release notes field (paste this)

For: *“Describe the changes made to the indicator…”* (appears under the description).

```
v14.1 update

• ORB column: Above/Below/Inside vs 5, 15, or 30 min opening range from 9:30 ET (one window at a time)
• Optional Filter ORB; Show/Color toggles like PrevD / PreMkt
```

Shorter alternative:

```
v14.1: ORB Above/Below/Inside for 5/15/30 min opening range (one at a time).
```

---

## Ready-to-paste revised description

Copy below into the TradingView publishing form when you promote v14.

---

## (v14 notes retained below for full republish)

```
v14 update

• Per-ticker On/Off — disable any watchlist slot without clearing the symbol (easier to monitor a smaller set)
• Optional sort: Score with PrevD / PreMkt ranges (default off) — names Above prior-day and/or premarket ranges rank above faster movers still Inside those ranges
• Optional Show table before RTH open (default off) — see Mov / PrevD / PreMkt in premarket; Open % and RS still appear after 9:30
• Reduced status-line clutter by hiding input values from the status line / Data Window (Settings → Inputs unchanged)
```

Shorter alternative:

```
v14: On/Off per ticker; optional PrevD/PreMkt range scoring for sort (off by default); optional premarket table (off by default); cleaner status line (input values hidden).
```
### Overview

This indicator compares a watchlist of up to 18 tickers against a benchmark (QQQ, SPY, SMH, IWM, or any custom symbol) and displays the results in a single on-chart table. It's built for intradayers who want a fast way to see which names are leading or lagging the broader market right now, rather than checking each symbol’s chart individually.

By default the script fetches up to **10** enabled symbols (adjustable) to stay within Pine’s request limits. Each ticker slot has an **On** checkbox so you can leave symbols configured but hide them from the table.

### How It Works

Every value in this table is computed from intraday bars tracked session-by-session — not from a separate daily-resolution lookup. The script watches the regular session (9:30–4:00 ET) and premarket (4:00–9:30 ET) directly, bar by bar, and locks in levels (prior-day high/low, premarket high/low, the first 5-minute range) when each session boundary is crossed. This avoids a common source of error in multi-symbol scripts where a separately resolved daily-timeframe request can return values that aren’t aligned with the rest of the script’s calculation.

The table includes:

- **Mov / Open** — % change from yesterday’s close, and separately from today’s regular open, so you can see whether a move happened overnight or during the session
- **RS** — whether the symbol’s since-open performance is outpacing, lagging, or in line with the benchmark
- **ADX** — trend strength via Wilder’s DMI (`ta.dmi`), with optional color by strength and DI+/DI− so a strong reading is distinguishable as bullish or bearish
- **RVOL** — current bar volume vs a volume SMA on the chart timeframe (default length 14), as a rough participation check, with configurable high / low color thresholds
- **PrevD / PreMkt / ORB** — whether price is currently Above, Inside, or Below the prior day’s range, the premarket range, and the selected opening range (5 / 15 / 30 min from 9:30 ET)
- **Trend** — Long / Short / Flat from PrevD + PreMkt + RS alignment (3/3 = strong, 2/3 = developing, mixed = Flat)
- **YTrend** — classifies yesterday’s session as a breakout, breakdown, or inside day relative to the range two sessions back
- Optional columns for the underlying price levels (PDH/PDL, PMH/PML, first-5-minute high/low)

### Settings (high level)

- **Benchmark:** QQQ / SPY / SMH / IWM or custom
- **Tickers:** up to 18 slots with per-slot **On** enable; **Max symbols to fetch** (default 10)
- **Sort:** strongest→top; sort by RS vs benchmark or Open %; optional **Score with PrevD / PreMkt ranges** (default off)
- **Show table before RTH open** (default off) for premarket context
- Column show/color toggles; PrevD / PreMkt / ORB / ADX **row filters**; ADX timeframe, thresholds, and optional ADX alerts
- RVOL length and high/low thresholds
- Table position, text size, dark/light theme

### How to Read It

The benchmark can be shown as a pinned reference row at the top. Below it, the watchlist is sorted by strength against that benchmark by default (RS or Open %). With **Score with PrevD / PreMkt ranges** enabled, names Above those ranges rank above faster movers still Inside — breakout structure is prioritized over raw speed alone.

A name showing RS agreement, a rising ADX in the same direction, and elevated RVOL is showing more conviction than a name that agrees on direction alone — read the columns together. Any single column can mislead (e.g. a strong day-over-day Mov with little activity since the open).

### Notes

This is a context and screening tool, not a buy/sell signal generator — it doesn’t predict future performance, and relative strength today doesn’t guarantee continuation. Combine with your own analysis and risk management. Designed for intraday use. By default, Open % and RS (and the table itself) appear after the regular session starts; turn on **Show table before RTH open** if you want Mov / PrevD / PreMkt context in premarket (Open % / RS still blank until 9:30).

---

## Checklist before publishing on TV

- [ ] Paste revised Overview (or merge the correction table + What’s new into your existing copy)
- [ ] Bump script version / title if required by your publishing workflow
- [ ] Confirm Settings screenshots match new toggles (On, Score with ranges, Show before RTH open)
- [ ] Push + compile from `scripts/v14/daily_trender.pine`
