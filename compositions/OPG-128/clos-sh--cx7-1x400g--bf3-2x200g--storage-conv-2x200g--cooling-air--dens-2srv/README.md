# OPG‑128 — Single‑Homed Clos (CX7 1×400G, BF3 2×200G, Converged Storage, Air, 2 srv/rack)

This variant matches the single‑homed OPG‑M exemplar for the backend. Each server’s backend links terminate on one leaf (8 servers per leaf); frontend remains L3 multihomed.

Why choose it
- Operational simplicity and clear failure domains; aligns tightly with OPG‑M.
- Predictable cross‑leaf behavior; good for staged adoption.

Attributes
- Backend: single‑homed Clos (per‑server backend on one leaf)
- Scale‑out NICs: CX7 1×400G per GPU
- Frontend NICs: BF3 2×200G per server (L3MH)
- Storage: converged, 2×200G per server
- Cooling/Density: air‑cooled; ~2 servers/rack (representative)
- Optics and zoning as per DS5000 guidance (4×200G on odd ports; 2×400G unrestricted; reserve 32×800G uplinks/leaf)

Assets
- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000‑based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

How to use
- Import `netbox_inventory.json` (optional), review diagrams, then apply wiring with Hedgehog.
- Expect more leaf‑spine load than rail‑optimized when tenants span many hosts; plan scheduling accordingly.

See also
- Size overview: ../README.md
- Compositions overview: ../../README.md
