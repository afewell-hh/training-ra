# XOC‑512 / 1× OPG‑512 — Rail‑Optimized Clos (Air)

Rail‑optimized backend with converged frontend. Domain‑local placement keeps most collectives leaf‑local, reducing spine traffic across the composition.

Attributes
- Backend: rail‑optimized; CX7 1×400G per GPU
- Frontend: BF3 2×200G (L3MH); storage converged
- Cooling/Density: air; ~2 servers/rack

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — HNP topology plan input (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
