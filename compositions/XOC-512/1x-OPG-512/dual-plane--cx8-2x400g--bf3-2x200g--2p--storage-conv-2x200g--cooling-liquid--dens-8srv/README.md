# XOC‑512 / 1× OPG‑512 — Dual‑Plane (Liquid)

Liquid‑cooled, higher density version of the dual‑plane backend.

Attributes
- Backend: dual plane (2p); CX8 2×400G per GPU
- Frontend: BF3 2×200G (L3MH)
- Cooling/Density: liquid; ~8 servers/rack

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
