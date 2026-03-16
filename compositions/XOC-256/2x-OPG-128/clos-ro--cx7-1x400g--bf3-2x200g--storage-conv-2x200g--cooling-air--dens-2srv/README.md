# XOC‑256 / 2× OPG‑128 — Rail‑Optimized Clos (Air)

Overview
- Bundles two OPG‑128 building blocks with an XOC spine layer. Rail‑optimized backend plus converged frontend. With domain‑local placement, most scale‑out stays leaf‑local, materially reducing spine traffic.

Attributes
- Backend: rail‑optimized; CX7 1×400G per GPU
- Frontend: BF3 2×200G per server (L3MH); storage converged
- Cooling/Density: air; ~2 servers/rack

Assets
- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000‑based)
- `wiring/` — Hedgehog Wiring CRDs (per fabric)
- `diagrams/` — visuals (per fabric)
- `netbox_inventory.json` — NetBox inventory export

Notes
 
See also
- Tier overview: ../../README.md
- Compositions overview: ../../../README.md
