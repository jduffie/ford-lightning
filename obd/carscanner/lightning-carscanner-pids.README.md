# lightning-carscanner-pids.torque.csv

Torque-format custom-PID file — the **importable** artifact. Load it in Car
Scanner via **Settings → custom PIDs → import** (or adapt through the forum
Torque templates). The `*-pids.csv` files in each dashboard folder are the
human-auditable record; this one is what you actually import.

> Verified on-vehicle 2026-06-13 — 2025 F-150 Lightning Flash (123 kWh),
> OBDLink MX+ (Bluetooth Classic) + Car Scanner iOS.

## Included (verified)

- HVB State of Charge — `0x224801`
- HVB State of Charge Displayed — `0x224845` (header `7e4`)
- HVB Voltage — `0x22480d` (header `7e2`)
- HV Current — `0x22480b` (header `7e2`)
- HVB Temperature — `0x224800`
- HVB Energy to Empty — `0x224848`
- HVB Power — computed (`HVB Voltage` × `HV Current`)

## Still TODO (not in this file)

State of health, 12V (LVB) SOC/voltage, motor/inverter temps — no verified hex
yet. To fill them, run `/fill-pids` and paste the rows from the source threads.
Never guess hex.

## Sources

- https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
- https://www.macheforum.com/site/threads/ford-mustang-mach-e-extended-pids-for-torque-project.7427/
