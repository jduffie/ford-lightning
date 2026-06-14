# Battery dashboard

High-voltage battery (HVB) state for the F-150 Lightning, plus the 12V (LVB).
9 tiles — under the CarPlay 10-PID cap.

> **Verified on-vehicle 2026-06-13** — 2025 F-150 Lightning Flash (123 kWh pack),
> OBDLink MX+ (Bluetooth Classic) + Car Scanner iOS. The HVB PIDs below read live
> on this truck — the 2025 Flash is **not** OBD-firewalled. Values captured at ~63%
> displayed SOC, charger unplugged, truck in Ready. Hex/formulas confirmed against
> the MachEforum PID sheet and cross-checked against the live readings.

## PID definitions

| Parameter | Header | Command | Formula | Unit | Live | Status |
|---|---|---|---|---|---|---|
| HVB State of Charge | (default) | `0x224801` | `INT16(A:B)*0.002` | % | 60.4 | ✅ verified |
| HVB pack voltage | `7E2` | `0x22480D` | `INT16(A:B)*0.01` | V | 343 | ✅ verified |
| HVB pack current | `7E2` | `0x22480B` | `((signed(A)*256)+B)*0.02` | A | 4.4 | ✅ verified |
| HVB power | — | computed | `val{HVB pack voltage}*val{HVB pack current}*0.001` | kW | 2.2 | ✅ computed |
| HVB pack temperature | (default) | `0x224800` | `(A-50)*1.8+32` | °F | 93.2 | ✅ verified |
| HVB state of health | (default) | `0x22490C` | `A*0.5` | % | 100 | ✅ verified |
| HVB energy to empty | (default) | `0x224848` | `INT16(A:B)*0.002` | kWh | 76.08 | ✅ verified |
| 12V (LVB) State of Charge | (default) | `0x224028` | `A` | % | — | 🟡 sheet |
| 12V (LVB) voltage | (default) | `0x22402A` | `A*0.05+6` | V | ~13.3 | ✅ verified |

Status: **✅ verified** = sheet hex + cross-checked against a live reading.
**🟡 sheet** = sheet hex with plausible scale, but no live value was captured to
cross-check (LVB SOC) — confirm opportunistically.

## Byte & function conventions

- `A, B, C, D` — data bytes of the mode-22 positive response, in order.
- `INT16(A:B)` = `A*256 + B` (unsigned 16-bit).
- `signed(A)` — two's-complement signed byte (so pack current goes negative on
  regen / charge).
- `val{Name}` — the live value of another PID (used by computed PIDs).
- **Header** — the request CAN ID (ECU). `(default)` = the Lightning profile's
  default request; confirm the header if you import the PID standalone.

## Layout / order (most-important first, ≤10 — CarPlay cap)

1. HVB State of Charge
2. HVB pack voltage
3. HVB pack current
4. HVB power (computed)
5. HVB pack temperature
6. HVB state of health
7. HVB energy to empty
8. 12V (LVB) State of Charge
9. 12V (LVB) voltage

## Notes

- Units are **°F** (app set to imperial). Car Scanner also exposes `HVB State of
  Charge Displayed` (`0x224845`, header `7E4`, `A*0.5`) — the buffered % the cluster
  shows (63% live vs 60.4% true SOC). Swap it in if you want the dash number.
- **HVB power** is computed from the two tiles above. The MachEforum sheet's native
  "HV Battery Power Flow Calculated" instead multiplies `HVB Voltage` by `HVB Current
  Low Range` (`0x22480A`) — equivalent; cross-checks to the native `HV EV Battery
  Power` reading (2.98 hp = 2.2 kW at 343 V × 6.5 A).
- All 9 tiles now carry hex from the compiled Ford BEV PID sheet (downloaded CSV).
  SOH (`0x22490C`) and 12V voltage (`0x22402A`) cross-check against live readings;
  LVB SOC (`0x224028`) is sheet-sourced (plausible scale, no live value captured).

## Screenshots

Phone view below is a Car Scanner **"All sensors" capture** from the on-vehicle test
(2025 Flash) — real readings, swappable for a built-dashboard view later. CarPlay
shot still pending.

![Battery — phone](../../assets/battery-phone.png)
<!-- ![Battery — CarPlay](../../assets/battery-carplay.png) -->
