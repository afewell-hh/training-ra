# XOC‑256 / 1× OPG‑128 — Rail‑Optimized Clos (Air)

Composes one OPG‑128 with a spine layer (XOC structure), using a rail‑optimized backend and converged frontend. With domain‑local placement, most scale‑out remains leaf‑local, materially reducing spine traffic.

Attributes
- Backend: rail‑optimized; CX7 1×400G per GPU
- Frontend: BF3 2×200G per server (L3MH); storage converged
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
