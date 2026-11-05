# Daily Trender v15.0.0

Based on **v14** / **v13.0.0-rc2** with ORB column and compact Tiny/Small labels.

## What’s new in v15

### ORB Settings

- **Show ORB** — Above / Below / Inside vs the selected opening-range high/low (same style as PrevD / PreMkt)
- **ORB minutes** — only one window at a time: **5** (09:30–09:35), **15** (09:30–09:45), **30** (09:30–10:00) ET
- Header label is `ORB5`, `ORB15`, or `ORB30`
- Optional **Filter ORB** — keep rows matching Above / Below / Inside
- Not part of Trend scoring or “Score with PrevD / PreMkt ranges”

### Compact labels (Tiny / Small)

When **Table Text Size** is Tiny or Small, status cells abbreviate:

| Full | Compact |
|------|---------|
| Above / Below / Inside | A / B / I |
| Long / Short / Flat | L / S / F |

Normal and Large keep full words. Filters and colors still use full labels internally.

## From v14

### Tickers — Enable (On)

Each ticker row has an **On** checkbox. Uncheck to remove that symbol from the table without clearing the field.

### Score with PrevD / PreMkt ranges (Settings)

- Default **off** — sort is RS vs benchmark or Open % only
- When **on** — primary sort by range breakout points (PrevD Above +1, PreMkt Above +1), then secondary RS/Open %

### Show table before RTH open (Settings)

- Default **off** — table appears after 9:30 ET when Open % is available
- When **on** — rows show in premarket if price is available

## Settings groups

### ADX / Previous Day / Pre Market / ORB / RVOL

Same show / color / filter pattern as v13–v14; ORB adds the minutes selector.

## Request limit (RE10137)

Pine allows **40 unique `request.*()` calls** per script. v15 requests the **benchmark + all 18 ticker slots at global scope** (19 calls) so `f_symbolBundle` is never inside a loop (CW10003). **Max symbols** only caps how many enabled rows appear in the table.

## Push

```bash
node src/cli/index.js pine set --file indicators/daily-trender/scripts/v15/daily_trender.pine
node src/cli/index.js pine compile
```
