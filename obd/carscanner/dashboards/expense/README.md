# Expense dashboard

Car Scanner has **no native EV cost feature**. This dashboard estimates trip cost
with a virtual PID built from energy used and a user-set `$/kWh` rate. 3 tiles —
well under the CarPlay 10-PID cap.

## PID definitions

| Parameter | Header | Mode+PID | Formula | Unit | Status |
|-----------|--------|----------|---------|------|--------|
| Energy used (trip) | TODO | TODO | TODO | kWh | TODO — from PID sheet |
| Trip cost | — | virtual | `energy_used × RATE` | $ | computed (input + rate TODO) |
| Speed | TODO | TODO | TODO | mph | TODO — from PID sheet |

`RATE` = `$/kWh`, a **documented, user-editable constant** you set in the trip-cost
PID's equation (e.g. a `$0.15` literal). It is **not** read from the car.

## Rate — where it comes from

The canonical `$/kWh` rate lives in **home-charging › `rates/`**. This dashboard
**points** to it — it does not own the number. Copy the rate from there into the
`RATE` constant.

Dependency direction is vehicle → home-charging. Never the reverse.

> home-charging ↗ `rates/` _(scaffold)_

## Layout / order

Most-important first:

1. Trip cost ($)
2. Energy used (kWh)
3. Speed (mph)

Speed is included so you can eyeball power-vs-speed (efficiency) alongside cost.

## Limits — read these

- **Flat rate only.** No home vs DC-fast-charge split — one `$/kWh` for everything.
- **Ignores charging losses.** Cost is computed from energy *used while driving*,
  not energy *drawn from the wall*. Real charging is ~10–15% higher due to
  AC/DC and thermal losses; this estimate runs low.
- **Estimate, not a bill.** No demand charges, no time-of-use tiers, no taxes/fees.

## Notes

- **Trip cost** is a virtual/computed PID: `energy_used × RATE`. Structurally
  defined now; produces real numbers once the energy-used PID hex is verified and
  the rate constant is set.
- Verify every `TODO` hex (energy used, speed) against the community PID sheets:
  - https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
  - https://www.macheforum.com/site/threads/tips-on-using-carscanner-elm-app-with-obd2-for-custom-data-display-ver-1-87-1-and-later.12627/
  The Lightning shares the Mach-E mode-22 PID set.

## Screenshots

_Screenshot pending._

![Expense — phone](../../assets/expense-phone.png)
![Expense — CarPlay](../../assets/expense-carplay.png)
