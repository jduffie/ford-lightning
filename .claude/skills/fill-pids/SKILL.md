---
name: fill-pids
description: "Fill verified PID hex from the forum sheets into the dashboard CSVs/READMEs, replacing TODO/UNVERIFIED. Use when the user asks to fill or verify PIDs."
disable-model-invocation: true
---

# fill-pids

Fill verified PID hex into the dashboards. NEVER guess hex — every value comes
from a source sheet or a value the user pasted.

## Open items

!`grep -rn "TODO\|UNVERIFIED" obd/carscanner/dashboards/`

## Steps

1. Show the open items above so the user sees what still needs hex.
2. Ask the user to paste the PID rows — **Name, Header, Command, Equation, Min,
   Max, Unit** — from the two source threads:
   - https://www.f150lightningforum.com/forum/threads/pid-list-to-monitor-your-lightning.13563/
   - https://www.macheforum.com/site/threads/ford-mustang-mach-e-extended-pids-for-torque-project.7427/
   (Forums are Cloudflare-walled and the Sheet isn't machine-fetchable — the
   human pastes; you never scrape-guess.)
3. Match each pasted row to its dashboard target (the TODO/UNVERIFIED row).
4. VALIDATE the formula against any known live value BEFORE writing — e.g. pack
   voltage must compute to ~343 V, displayed SOC to the cluster %. If it doesn't
   check out, stop and flag it; don't write it.
5. Update BOTH places for each filled PID:
   - the dashboard `README.md` table, and
   - the matching `*-pids.csv` (keep columns uniform — 10 cols).
6. Keep ≤10 PIDs per page. Recompute any computed-PID inputs (e.g. power = V·I)
   if their source PIDs changed.
7. Leave anything you can't cite as `TODO`/`UNVERIFIED`, and report what's still
   open at the end.
