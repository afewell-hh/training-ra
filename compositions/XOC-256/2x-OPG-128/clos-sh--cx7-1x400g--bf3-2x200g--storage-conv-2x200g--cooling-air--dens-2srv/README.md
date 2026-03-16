# XOC‑256 / 2× OPG‑128 — Single‑Homed Clos (Air)

Overview
- Two OPG‑128 building blocks with a single‑homed backend per OPG and a converged frontend.

Why choose it
- Simpler host semantics at XOC scale; good for staged adoption when rail constraints are not desired.

Attributes
- Backend: single‑homed; CX7 1×400G per GPU
- Frontend: BF3 2×200G per server (L3MH)
- Cooling/Density: air; ~2 servers/rack

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
