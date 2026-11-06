# Hood Boss QA Brain // Master Control v2

A separate master control page. It does **not** replace the live QA Brain
(`AntManThePro/HBQAbrain`, served at hbqabrain.netlify.app).

## What it is

A single-file, offline command layer that observes upstream systems. It
correlates imported jobs, readiness, recurring defects and operational
events into one traceable view. It does not silently overwrite any
authoritative system's records. Imported events stay traceable to source
and timestamp.

- Event ledger (append-oriented, local only)
- Job intelligence with filter
- Pattern engine with evidence thresholds
- 10-agent synthesis — scores are a **derived triage index from overall
  operational health, not independent per-agent measurements**
- Escalation routing queue
- Adapter fabric + normalized event contract
- Readiness view

## Data

- No live connections. Adapters are listed as READY/ACTIVE labels only;
  nothing is fetched from FieldPulse, Field Monitor, Team Lead OS or
  Scorecard yet.
- Data arrives by importing a JSON pack, or by loading the explicitly
  synthetic demo dataset (5 jobs, labelled DEMO — SYNTHETIC DATA).
- Imported data is saved in the browser under localStorage key
  `qa-brain-v2-ledger` and restored on reload. Clear Local Ledger wipes it.

## Files

- `index.html` — cleaned copy (audit fixes applied, see below)
- `qa-brain-master-v2-original.html` — the pasted original, untouched
- `manifest.json`, `favicon.ico`, `icons/` — custom QB icon set

## Audit fixes in the cleaned copy

- localStorage persistence (save after import/demo/clear/synthesis,
  restore on boot)
- Evidence coverage: third checkpoint is now photos present, not
  `deficiency >= 0` (which was always true)
- Adapter count reads "1 ACTIVE · 6 READY", not "7 ACTIVE"
- Resize handler redraws the risk chart; canvas null-context guard
- Per-job counts take priority over pack-level counts
- People deduped by name/id on import
- `uid()` fallback when `crypto.randomUUID` is unavailable
- Ledger retitled "Append-oriented" — Clear wipes it, so it is not immutable

## Deploy

- Branch: `main`, publish directory: root, build command: none
- Intended as a private Netlify site under Team login, like the other
  Hood Boss manager sites — not public.

## Verification (2026-11-06, local)

- JS syntax check passes; local serve HTTP 200 for index, favicon,
  manifest and icon-512.
- DOM test: empty state 0 jobs; demo 5 jobs / health 79% / coverage 93% /
  7 signals / 2 critical; synthesis shows 10 agent cards; job filter
  "Buda" returns 1 row; event Inspect modal opens/closes; escalation
  7 items; ledger persists across reload.
- Real phone test still needed.
