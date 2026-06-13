# Roadmap

Interest-gauged. Each item below is a draft GitHub issue body. The owner opens the
issues; readers **👍 to vote**. **Nothing here is built until it's voted.**

---

## EVScanner support

**Body:**

Add EVScanner dashboards for the F-150 Lightning, mirroring the Car Scanner
battery/performance/expense set. Same mode-22 PID set (shared with the Mach-E),
re-packaged for EVScanner's import format. Would add EVScanner's cell-level and
state-of-health views where they show more than Car Scanner can.

Scope if voted:
- Port the verified PIDs into EVScanner's custom-PID format.
- One dashboard per category, parity with the Car Scanner pages.
- Document the EVScanner import flow.

Depends on: the Car Scanner PID hex being verified first (shared source of truth).

**👍 to vote.**

---

## Cost pipeline (consumes home-charging data)

**Body:**

Replace the flat-rate trip-cost estimate with a real pipeline. Pull the canonical
`$/kWh` from **home-charging › `rates/`** automatically (instead of a hand-copied
constant), and optionally reconcile against actual charging sessions so cost
reflects energy drawn from the wall — including charging losses and a home vs
DC-fast-charge split.

Scope if voted:
- Read the rate from home-charging rather than a literal in the PID equation.
- Account for charging losses (driving-energy vs wall-energy gap).
- Split home vs DCFC pricing.
- Keep dependency direction vehicle → home-charging.

Depends on: home-charging `rates/` being populated (currently scaffold).

**👍 to vote.**

---

_Also tracked here: Android / Android Auto support for the dashboards — "on
request." Open an issue if you want it._
