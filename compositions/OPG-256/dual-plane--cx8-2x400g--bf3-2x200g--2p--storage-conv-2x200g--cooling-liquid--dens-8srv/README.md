# OPG‑256 — Dual‑Plane Backend (CX8 2×400G, BF3 2×200G, Converged Storage, Liquid, 8 srv/rack)

Liquid‑cooled, higher‑density variant of the OPG‑256 dual‑plane backend. Networking characteristics are identical to the air‑cooled option.

Attributes
- Backend: dual plane (2p); CX8 2×400G per GPU
- Frontend: BF3 2×200G per server (L3MH)
- Storage: converged, 2×200G per server
- Cooling/Density: liquid‑cooled; ~8 servers/rack (placeholder)
- Optics/Zoning: per DS5000 guidance; maintain uplink budgets across planes

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
