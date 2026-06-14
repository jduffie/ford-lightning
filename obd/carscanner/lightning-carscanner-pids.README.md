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
- HVB State of Health — `0x22490c`
- LVB State of Charge (12V) — `0x224028`
- LVB Voltage (12V) — `0x22402a`
- Primary Motor Coil Temperature — `0x22481f`
- Primary Motor Inverter Temperature — `0x224824`
- HVB Power — computed (`HVB Voltage` × `HV Current`)

## Verification

All 12 PIDs carry hex from the compiled Ford BEV PID sheet. Most are cross-checked
against live on-vehicle readings; LVB SOC and the two motor temps are sheet-sourced
(plausible scale, no live value captured). None are guessed.

## Sources

- https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
- https://www.macheforum.com/site/threads/ford-mustang-mach-e-extended-pids-for-torque-project.7427/
