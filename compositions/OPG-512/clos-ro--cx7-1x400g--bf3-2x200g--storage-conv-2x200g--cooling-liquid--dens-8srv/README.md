# OPG‑512 — Rail‑Optimized Clos (CX7 1×400G, BF3 2×200G, Converged Storage, Liquid, 8 srv/rack)

Liquid‑cooled, higher‑density variant; networking matches the air‑cooled option.

Why choose it
- Reduce spine congestion at higher OPG scale by keeping collectives leaf‑local when placement aligns with rail domains.
- Liquid‑cooled density reduces racks and cable runs while preserving the same wiring logic.

Attributes
- Backend: rail‑optimized Clos; CX7 1×400G per GPU
- Frontend: BF3 2×200G per server (L3MH)
- Storage: converged, 2×200G per server
- Cooling/Density: liquid‑cooled; ~8 servers/rack (placeholder)

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
