# XOC‑256 / 1× OPG‑128 — Single‑Homed Clos (Air)

Single‑homed backend as per OPG‑M exemplar; converged frontend.

Attributes
- Backend: single‑homed; CX7 1×400G per GPU
- Frontend: BF3 2×200G per server (L3MH)
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
