# ford-lightning

Owner hub for the **2025 F-150 Lightning Flash**. A task index — find your
question, follow the one link.

> A BEV on the Ford Mustang Mach-E / F-150 Lightning platform. OBD via **OBDLink
> MX+ (Bluetooth Classic)** + **Car Scanner (iOS)**. PID sources: the F-150 Lightning
> Forum and MachEforum community PID sheets.

## I own an F-150 Lightning. How do I…?

| Question | Answer | Link |
|----------|--------|------|
| …see battery state (SOC, voltage, temp, health) in real time? | Import the Battery dashboard into Car Scanner. | [obd/carscanner → Battery](obd/carscanner/dashboards/battery/) |
| …watch performance (power, current, motor/inverter temps)? | Import the Performance dashboard. | [obd/carscanner → Performance](obd/carscanner/dashboards/performance/) |
| …estimate what a trip cost in electricity? | Import the Expense dashboard (uses a `$/kWh` rate you set). | [obd/carscanner → Expense](obd/carscanner/dashboards/expense/) |
| …get Car Scanner set up and these dashboards loaded? | Restore-from-backup install flow. | [obd/carscanner/install.md](obd/carscanner/install.md) |
| …know the right `$/kWh` rate to use for cost? | That lives in home-charging (canonical rate). | [home-charging ↗ `rates/`](https://github.com/jduffie/home-charging/tree/main/rates) |
| …size or install a home charger for this truck? | Situational — copy the prompt into an LLM. | [home-charging ↗ charger-sizing prompt](https://github.com/jduffie/home-charging/blob/main/prompts/charger-sizing.md) |
| …use EVScanner instead of Car Scanner? | Future. 👍 to vote. | [obd/evscanner](obd/evscanner/) |
| …do this on Android / Android Auto? | On request — open an issue. | [docs/roadmap.md](docs/roadmap.md) |

Topics beyond OBD (charging, cost pipeline, …) are **TBD** — they appear here as
lines that resolve to local content, a pointer, or a prompt. The reader doesn't
care which.

## Status

`obd/carscanner` is built and **verified on-vehicle (2026-06-13)** on a 2025 Flash
(123 kWh) with an OBDLink MX+ — full HVB / motor / 12V telemetry reads, so the 2025
Flash is **not** OBD-firewalled. All Battery/Performance PIDs are filled with hex
from the Ford BEV PID sheet — most cross-checked against live readings, a few (LVB
SOC, motor/inverter temps) sheet-sourced. See each dashboard's table.
