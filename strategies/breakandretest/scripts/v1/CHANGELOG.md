# Break and Bounce — v1.0.0

## v1.0.0 — 2025-06-19

Initial implementation per `docs/break_and_bounce_spec.md`:

- §2 PDH/PDL daily levels (non-repainting)
- §3 5m breakout with dual displacement modes + RVOL gate
- §4 Session filter (9:30–11:30 ET), retest timeout SM, first-retest rule
- §5 Volume quadrant + internal relational confluence (thresholds PENDING CALIBRATION)
- §6–9 Entry, structural SL (close-confirmed), circuit breaker (intrabar), 2R TP
- Visualization: PDH/PDL plots, retest box, entry/SL/TP/CB lines, debug table
- `log.info()` on every state transition for MCP `pine_get_console` debugging

**Test on:** 5-minute chart only. Default retest TF = 1m.

**Locked defaults:** body 50%, ATR mult 1.0, session window, 2R TP, pivot SL logic.

**Open for sweep:** all §5.3 volume thresholds, circuit breaker %, displacement mode default.
