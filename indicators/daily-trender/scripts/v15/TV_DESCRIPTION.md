# TradingView description updates — Daily Trender v15

Source: `indicators/daily-trender/scripts/v15/daily_trender.pine` (v15.0.0).

---

## Paste into TradingView — “Describe the changes…” (release notes)

```
v15.0.0

• ORB column: Above/Below/Inside vs opening range from 9:30 ET — choose 5, 15, or 30 minutes (one window at a time). Header: ORB5 / ORB15 / ORB30. Optional Show / Color / Filter like PrevD / PreMkt.
• Compact labels when Table Text Size is Tiny or Small: Above→A, Below→B, Inside→I, Long→L, Short→S, Flat→F (Normal/Large stay full words).
```

### Shorter alternative

```
v15: ORB (5/15/30 min from 9:30 ET) Above/Below/Inside column + compact A/B/I/L/S/F labels for Tiny & Small table text.
```

---

## What’s new in v15 (for Overview if you republish)

1. **ORB column** — price vs opening-range high/low from 9:30 ET. Select **5**, **15**, or **30** minutes (only one active). Optional filter Above / Below / Inside.
2. **Compact labels** — Tiny/Small table text uses A/B/I and L/S/F; Normal/Large keep full words.

### Still from v14 (mention if not already on the published Overview)

- Per-ticker **On** toggle
- Optional **Score with PrevD / PreMkt ranges** (default off)
- Optional **Show table before RTH open** (default off)
- Cleaner status line (`display.none` on non-bool inputs)

---

## Ready-to-paste Overview snippet (ORB + compact)

Add under columns / settings:

- **ORB** — Above, Inside, or Below the selected opening range (5 / 15 / 30 min from 9:30 ET); optional row filter
- Table text **Tiny/Small**: compact A / B / I / L / S / F; Normal/Large: full labels
