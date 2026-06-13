# Car Scanner setup + dashboard import

Get Car Scanner talking to the Lightning, then load the dashboards.

> **Verified 2026-06-13** on a 2025 F-150 Lightning Flash (123 kWh) with an OBDLink
> MX+ + Car Scanner iOS: full HVB / dual-motor / 12V telemetry reads — the 2025 Flash
> is **not** OBD-firewalled. The truck must be in **Ready** to stream live data.

## Platforms

- Car Scanner iOS (iPhone) + iOS CarPlay.
- **Android / Android Auto on request** — open an issue.

## 1. Pair the adapter

1. Plug the **OBDLink MX+** into the OBD-II port (driver-side, under the dash).
2. **One-time:** open the **OBDLink app**, update the MX+ firmware, then **fully
   force-quit** it — if it stays alive it holds the Bluetooth link and blocks Car
   Scanner. Don't reopen it.
3. iOS **Settings → Bluetooth** → pair the MX+. The MX+ is **Bluetooth Classic
   (BT 3.0), not BLE.**
4. In Car Scanner → **Settings → Connection** set adapter type to **Bluetooth (3.0)**
   (not Bluetooth LE), select the MX+, and connect.
5. Connection profile: **Mustang Mach-E / F-150 Lightning / E-Transit**.

> Adapter note: the MX+ reads the documented HVB PIDs fine via the OBD-II gateway.
> The OBDLink **CX** (BLE 5.1) is the other common pick if you want BLE pairing or
> CAN-FD raw-bus access — but it is **not** required for these dashboards.

## 2. Import the dashboards (Restore from Backup)

The community shares full Lightning dashboards as a Car Scanner **backup** (`.cbz`),
so the import is a **restore**. (Car Scanner also has a per-dashboard Save/Restore;
the `.cbz` backup is the method used by the forum templates.) A restore overwrites
settings — protect yours first.

1. **Back up your own settings first:** Settings → Backup → create a backup. Keep
   it. The restore in the next step replaces your current configuration.
2. **Restore from Backup:** Settings → Backup → **Restore from Backup** → choose
   the provided backup file. This loads the dashboards and their custom PIDs.
3. **Delete the bundled adapter:** the backup carries the original author's adapter
   entry. Settings → Connection → remove it.
4. **Re-pair your MX+** (step 1 above) so Car Scanner talks to *your* adapter.
5. **Re-backup:** create a fresh backup now that it has the dashboards + your
   adapter. That's your clean restore point.

## 3. CarPlay

CarPlay renders each dashboard page as a **text list capped at 10 PIDs**. Every
page here is ≤10 PIDs, most-important first, so it shows fully on the head unit.

## How the `*-pids.csv` files relate

Each dashboard folder has a `<category>-pids.csv`. **These document the custom-PID
set** (name, header, mode+PID, equation, range, unit, status) in a readable,
diff-able form — they are the human-auditable record of what each dashboard
contains and which cells still need verified hex.

They are **not** the install mechanism. The canonical install is the
**backup-restore** above; the CSVs are reference/source-of-record. If Car Scanner
later supports direct custom-PID CSV import on your build, the header row is
documented so they can be adapted.

An **importable Torque-format CSV** of the verified PIDs now exists at
[`lightning-carscanner-pids.torque.csv`](lightning-carscanner-pids.torque.csv)
(Settings → custom PIDs → import) — see its
[README](lightning-carscanner-pids.README.md).
