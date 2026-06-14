# Car Scanner — F-150 Lightning

Car Scanner + the OBDLink MX+ reads the Lightning's mode-22 PIDs (shared with the
Mach-E) and shows them as live dashboards on iPhone and CarPlay.

Setup and import flow: [install.md](install.md).

## Dashboards

| Category | What it shows | Page |
|----------|---------------|------|
| Battery | SOC, pack voltage/current/power, pack temp, health, energy, 12V | [dashboards/battery](dashboards/battery/) |
| Performance | Power (regen negative), current, voltage, motor/inverter temps, SOC | [dashboards/performance](dashboards/performance/) |
| Expense | Trip cost from a user-set `$/kWh`, kWh used, speed | [dashboards/expense](dashboards/expense/) |

## Notes

- **CarPlay caps each page at 10 PIDs** — every dashboard is ≤10, most-important
  first.
- Platforms: Car Scanner iOS (iPhone) + iOS CarPlay. **Android / Android Auto on
  request.**
- Adapter: **OBDLink MX+ (Bluetooth Classic, BT 3.0 — not BLE).** See
  [install.md](install.md).
- **Verified on-vehicle 2026-06-13** on a 2025 Flash: all Battery/Performance PIDs
  are now filled with hex from the Ford BEV PID sheet — most cross-checked against
  live readings, a few (LVB SOC, motor/inverter temps) sheet-sourced. Not firewalled.
