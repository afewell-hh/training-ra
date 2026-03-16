# XOC‑1024 / 2× OPG‑512 — Dual‑Plane (Liquid)

Higher density via liquid cooling; networking identical to air variant.

Attributes
- Backend: dual plane (2p); CX8 2×400G per GPU
- Frontend: BF3 2×200G (L3MH); storage converged
- Cooling/Density: liquid; ~8 servers/rack

Assets (partial — generation incomplete; needs fast-follow)
- `topology-map.yaml` — HNP topology plan input (DS5000-based)
- Pending: `connectivity-map.csv`, `wiring/`, `diagrams/`, `netbox_inventory.json`

Notes
- Wiring and NetBox export blocked by port-exhaustion gap at XOC-1024 scale; see generate.log.
