# Performance dashboard

Drivetrain power and thermals for the F-150 Lightning. 6 tiles — under the CarPlay
10-PID cap.

> **Verified on-vehicle 2026-06-13** — power, current, voltage and SOC read live on
> a 2025 Flash (OBDLink MX+ + Car Scanner). Motor/inverter temps weren't in the
> MachEforum Torque CSV we pulled — see TODO below.

## PID definitions

| Parameter | Header | Command | Formula | Unit | Live | Status |
|---|---|---|---|---|---|---|
| Instantaneous power | — | computed | `val{HVB pack voltage}*val{HVB pack current}*0.001` (regen negative) | kW | 2.2 | ✅ computed |
| HVB pack current | `7E2` | `0x22480B` | `((signed(A)*256)+B)*0.02` | A | 4.4 | ✅ verified |
| HVB pack voltage | `7E2` | `0x22480D` | `INT16(A:B)*0.01` | V | 343 | ✅ verified |
| Primary motor coil temperature | — | TODO | TODO | °F | — | ⚠️ TODO |
| Primary motor inverter temperature | — | TODO | TODO | °F | — | ⚠️ TODO |
| HVB State of Charge | (default) | `0x224801` | `INT16(A:B)*0.002` | % | 60.4 | ✅ verified |

Byte/function conventions (`INT16`, `signed`, `val{}`, `(default)` header) are
documented in [../battery/README.md](../battery/README.md#byte--function-conventions).

## Layout / order

Most-important first, ≤10 PIDs (CarPlay caps a page at 10):

1. Instantaneous power (kW, regen negative)
2. HVB pack current
3. HVB pack voltage
4. Primary motor coil temperature
5. Primary motor inverter temperature
6. HVB State of Charge

(Power leads — the number you watch while driving. Voltage and current feed it.)

## 0–60 / acceleration

**0–60 is not a PID.** Use Car Scanner's built-in tool: **Menu → Acceleration
measurement** (the dyno / 0–100 tool). It times 0–60 mph (and ¼-mile etc.) from the
speed signal. Caveat: it derives 0–60 from the speed signal, so it lags a dragstrip
and is sensitive to launch, grade, payload, and tire slip on a ~6,500 lb truck. Run
it on a closed course / safe road.

## Notes

- **Instantaneous power** is computed from the voltage and current tiles; sign
  follows current, so regen reads negative.
- Motor/inverter temps showed live in Car Scanner's built-in profile (rows
  `Primary Motor Coil Temperature` / `Primary Motor Inverter Temperature`) but weren't
  in the Torque CSV we verified. Pull their hex from:
  - https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
  - https://www.macheforum.com/site/threads/ford-mustang-mach-e-extended-pids-for-torque-project.7427/
- The Lightning is dual-motor — `Primary` (front) and `Secondary` (rear) each have
  coil + inverter temps. Add the rear pair if you want all four (watch the 10-PID cap).

## Screenshots

Phone view below is a Car Scanner **"All sensors" capture** from the on-vehicle test
(showing the primary motor coil/inverter temps) — swappable for a built-dashboard
view later. CarPlay shot still pending.

![Performance — phone](../../assets/performance-phone.png)
<!-- ![Performance — CarPlay](../../assets/performance-carplay.png) -->
