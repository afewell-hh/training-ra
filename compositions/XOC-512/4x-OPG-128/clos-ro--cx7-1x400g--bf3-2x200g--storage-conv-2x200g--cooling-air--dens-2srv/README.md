# XOC‑512 / 2× OPG‑128 — Rail‑Optimized Clos (Air)

Rail‑optimized across OPGs; when jobs are placed within first‑hop rail domains, collective traffic remains mostly leaf‑local, materially reducing spine utilization.

Attributes
- Backend: rail‑optimized; CX7 1×400G per GPU (per OPG)
- Frontend: BF3 2×200G (L3MH); storage converged per OPG
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
