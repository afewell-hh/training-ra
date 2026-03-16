# OPG‑512 — Dual‑Plane Backend (CX8 2×400G, BF3 2×200G, Converged Storage, Air, 2 srv/rack)

Two backend planes with CX8 2×400G per GPU (one port per plane) to increase bandwidth and allow plane‑level maintenance.

Attributes
- Backend: dual plane (2p); CX8 2×400G per GPU
- Frontend: BF3 2×200G per server (L3MH)
- Storage: converged, 2×200G per server
- Cooling/Density: air‑cooled; ~2 servers/rack (placeholder)

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — HNP topology plan input (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend-plane-a.yaml` — backend Plane A fabric wiring
  - `wiring-backend-plane-b.yaml` — backend Plane B fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend-plane-a.drawio` — backend Plane A topology (draw.io)
  - `hhfab/backend-plane-b.drawio` — backend Plane B topology (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
