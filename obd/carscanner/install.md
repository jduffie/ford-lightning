# Car Scanner setup + dashboard import

Get Car Scanner talking to the Lightning, then load the dashboards.

## Platforms

- Car Scanner iOS (iPhone) + iOS CarPlay.
- **Android / Android Auto on request** — open an issue.

## 1. Pair the adapter

1. Plug the **OBDLink MX+** into the OBD-II port (driver-side, under the dash).
2. iOS Bluetooth: pair the MX+ (BLE).
3. In Car Scanner → **Settings → Connection**, select the MX+ and connect.
4. Connection profile: **Ford Mustang Mach-E / F-150 Lightning**.

## 2. Import the dashboards (Restore from Backup)

Car Scanner has **no import-from-file** for dashboards. Dashboards travel inside a
**backup**, so the import is a restore. This overwrites settings — protect yours
first.

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
