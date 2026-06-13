# Expense dashboard

Estimate what a trip cost in electricity. 3 tiles — well under the CarPlay 10-PID cap.

> **Finding (2026-06-13):** Car Scanner actually has **native energy + cost sensors**
> — `Energy used` (kWh), `Energy costs` ($), and `EV Instant Energy Consumption`. So
> this page doesn't need a hand-built virtual PID: set your rate once and use the
> native cost sensor. The virtual `Energy used × RATE` is kept as a fallback.

## PID definitions

| Parameter | Source | Formula / how | Unit | Status |
|---|---|---|---|---|
| Energy used (trip) | Car Scanner native sensor | built-in `Energy used` | kWh | ✅ native |
| Trip cost | Car Scanner native sensor | native `Energy costs` (set `$/kWh` in Settings) — or virtual `val{Energy used}*RATE` | $ | ✅ native / virtual |
| Vehicle speed | Car Scanner native sensor | built-in `Vehicle speed` | mph | ✅ native |

These are **standard Car Scanner sensors**, not custom mode-22 PIDs — no hex to fill.

## Rate — where it comes from

Set the `$/kWh` once in Car Scanner (Settings → currency + energy price) so the native
`Energy costs` sensor computes cost. The **canonical** rate lives in
**home-charging › `rates/`** — copy it from there; this dashboard points to it, it
does not own the number. Dependency direction is vehicle → home-charging, never the
reverse.

> home-charging ↗ `rates/` _(scaffold)_

## Layout / order

Most-important first:

1. Trip cost ($)
2. Energy used (kWh)
3. Vehicle speed (mph)

Speed is included so you can eyeball power-vs-speed (efficiency) alongside cost.

## Limits — read these

- **Flat rate only.** No home vs DC-fast-charge split — one `$/kWh` for everything.
- **Ignores charging losses.** Cost is from energy *used while driving*, not energy
  *drawn from the wall*. Real charging runs ~10–15% higher (AC/DC + thermal losses);
  DCFC losses and idle/session fees differ again. This estimate runs low.
- **Estimate, not a bill.** No demand charges, no time-of-use tiers, no taxes/fees.

## Notes

- If you prefer the virtual route, `Trip cost = val{Energy used} * RATE`, where `RATE`
  is a `$/kWh` literal you paste from home-charging › `rates/`.
- For deeper cost tracking, `HVB Energy to Empty` (`0x224848`, verified) deltas give
  battery-out kWh between two points.

## Screenshots

_Screenshot pending — embeds commented out until the PNGs are committed._

<!-- ![Expense — phone](../../assets/expense-phone.png) -->
<!-- ![Expense — CarPlay](../../assets/expense-carplay.png) -->
