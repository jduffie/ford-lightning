# CLAUDE.md — ford-lightning

## Rules (every session)
- NEVER invent PID hex. Unverifiable → `TODO` (or `UNVERIFIED` citing a source).
  Filling verified hex is a deliberate, human-checked step. Computed PIDs
  (power = V·I) are fine only when their inputs are verified.
- ≤10 PIDs per dashboard page — CarPlay renders a page as a text list capped at
  10; most-important first.
- The `$/kWh` cost rate is owned by `home-charging/rates/`. This repo
  REFERENCES it, never defines it. Dependency direction: vehicle →
  home-charging, never the reverse.
- Situational / advice questions (charger sizing, install) → point to a prompt,
  never prose.
- Roadmap items are interest-gauged; don't build one until it's voted.

## This vehicle
2025 F-150 Lightning Flash, 123 kWh pack. BEV on the Ford Mustang Mach-E /
F-150 Lightning platform; shares the Mach-E mode-22 PID set. Adapter: OBDLink
MX+ (Bluetooth Classic — NOT BLE); OBDLink CX (BLE + CAN-FD) optional, not
required. App: Car Scanner iOS + CarPlay. Car Scanner profile: "Mustang
Mach-E / F-150 Lightning / E-Transit".

## Verified on-vehicle 2026-06-13
Full HVB / dual-motor / 12V telemetry reads on this truck — it is NOT
OBD-firewalled. Battery/Performance hex is confirmed and cross-checked against
live readings. Still TODO: state of health, 12V (LVB) SOC/voltage,
motor/inverter temps.

## Car Scanner PID conventions
- Custom-PID fields: Name, Short name, Header (request CAN ID e.g. 7E2; blank =
  profile default), Command (full hex e.g. 0x224801), Equation, Min, Max, Units.
- Equation bytes: A,B,C,D = response data bytes in order. INT16(A:B)=A*256+B.
  signed(A)=two's-complement byte. val{Name}=another PID's live value.
- The `*-pids.csv` files are the human-auditable record. The importable artifact
  is the Torque-format CSV
  (obd/carscanner/lightning-carscanner-pids.torque.csv) or a Car Scanner backup.

## PID sources
- https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
- https://www.macheforum.com/site/threads/ford-mustang-mach-e-extended-pids-for-torque-project.7427/
Note: these forums are Cloudflare-walled (WebFetch 403s) and the Google Sheet
isn't machine-fetchable — the human pastes the rows. Never scrape-guess hex.

## To fill the remaining PIDs: run `/fill-pids`.
Full repo standard lives in the garage-workspace work repo (STRUCTURE.md).
