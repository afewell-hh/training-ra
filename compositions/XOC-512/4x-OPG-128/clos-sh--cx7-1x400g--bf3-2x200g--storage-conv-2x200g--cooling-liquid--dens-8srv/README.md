# XOC‑512 / 4× OPG‑128 — Single‑Homed Clos (Liquid)

Overview
- Four OPG‑128 building blocks under an XOC spine layer. Single‑homed backend per OPG and converged frontend. Liquid cooling enables higher rack density.

Why choose it
- Simpler host semantics with higher density when liquid cooling is available.

Attributes
- Backend: single‑homed; CX7 1×400G per GPU
- Frontend: BF3 2×200G (L3MH)
- Cooling/Density: liquid; ~8 servers/rack

Assets
- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000‑based)
- `wiring/` — Hedgehog Wiring CRDs (per fabric)
- `diagrams/` — visuals (per fabric)
- `netbox_inventory.json` — NetBox inventory export

Notes
