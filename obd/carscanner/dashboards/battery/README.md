# Battery dashboard

High-voltage battery (HVB) state for the F-150 Lightning, plus the 12V (LVB).
9 PIDs — under the CarPlay 10-PID cap.

## PID definitions

| Parameter | Header | Mode+PID | Formula | Unit | Status |
|-----------|--------|----------|---------|------|--------|
| HVB State of Charge | `7E6` | `22 4801` | TODO — confirm scaling | % | UNVERIFIED — confirm against the PID sheet |
| HVB pack voltage | TODO | TODO | TODO | V | TODO — from PID sheet |
| HVB pack current | TODO | TODO | TODO | A | TODO — from PID sheet |
| HVB power | — | computed | `voltage × current ÷ 1000` | kW | computed (inputs TODO) |
| HVB pack temperature | TODO | `22 4800` | TODO — confirm scaling | °C | UNVERIFIED — confirm against the PID sheet |
| HVB state of health / age | TODO | TODO | TODO | % | TODO — from PID sheet |
| HVB pack energy | TODO | TODO | TODO | kWh | TODO — from PID sheet |
| 12V (LVB) State of Charge | TODO | TODO | TODO | % | TODO — from PID sheet |
| 12V (LVB) voltage | TODO | TODO | TODO | V | TODO — from PID sheet |

## Layout / order

Most-important first, ≤10 PIDs (CarPlay caps a page at 10):

1. HVB State of Charge
2. HVB pack voltage
3. HVB pack current
4. HVB power (computed V·I)
5. HVB pack temperature
6. HVB state of health / age
7. HVB pack energy
8. 12V (LVB) State of Charge
9. 12V (LVB) voltage

## Notes

- **Power** is a virtual/computed PID: `voltage × current ÷ 1000` → kW. The
  formula is structurally correct; it only produces real numbers once the pack
  voltage and current PIDs are verified and filled.
- The two `UNVERIFIED` rows (SOC `7E6`/`22 4801`, pack temp `22 4800`) are
  candidate addresses from the MachEforum thread — confirm before relying on them.
- Verify every `TODO`/`UNVERIFIED` hex against the community PID sheets:
  - https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
  - https://www.macheforum.com/site/threads/tips-on-using-carscanner-elm-app-with-obd2-for-custom-data-display-ver-1-87-1-and-later.12627/
  The Lightning shares the Mach-E mode-22 PID set.

## Screenshots

_Screenshot pending._

![Battery — phone](../../assets/battery-phone.png)
![Battery — CarPlay](../../assets/battery-carplay.png)
