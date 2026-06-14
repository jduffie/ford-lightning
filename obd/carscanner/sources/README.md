# PID sources

Provenance for the verified PID hex used in the dashboards.

## `compiled-ford-bev-pids.csv`

The community "Compiled Ford BEV PIDs" sheet, exported as CSV (96 PIDs). This is
the authoritative source the dashboard hex was pulled from, kept here so the
origins are auditable.

- Source threads:
  - https://www.macheforum.com/site/threads/ford-mustang-mach-e-extended-pids-for-torque-project.7427/
  - https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
- Pulled / cross-checked on a 2025 F-150 Lightning Flash (123 kWh) on 2026-06-13.

### ⚠️ Column gotcha (read before reusing this file)

The header is `Name,,Header,ModeAndPID,ShortName,Name,Equation,Min Value,Max Value,Units,…`
— there are **two `Name` columns**. Column 0 is a separate sorted list; the **real
PID identity is column 5** (the `Name` next to `ShortName`/`Equation`). Reading
column 0 will mis-pair a PID's label with another row's hex/formula. Cross-check
column 4 (`ShortName`) against column 5 (`Name`) — they should agree (e.g. `HvbSoh`
↔ `HVB State of Health`).

### Verification

Each PID used in the dashboards was taken from column 5 and, where a live reading
was captured, cross-checked against it (e.g. pack voltage → ~343 V, SOH → 100%).
PIDs with no captured live value (LVB SOC, motor temps) are marked `🟡 sheet` in the
dashboard tables. Nothing is guessed.
