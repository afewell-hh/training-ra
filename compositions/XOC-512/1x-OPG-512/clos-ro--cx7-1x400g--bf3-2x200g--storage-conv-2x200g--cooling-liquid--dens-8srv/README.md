# XOC‑512 / 1× OPG‑512 — Rail‑Optimized Clos (Liquid)

Higher density via liquid cooling; networking identical to air variant.

Why choose it
- Lower tail latency under load from reduced spine traffic with rail‑optimized placement; higher density when liquid cooling is available.

Attributes
- Backend: rail‑optimized; CX7 1×400G per GPU
- Frontend: BF3 2×200G (L3MH); storage converged
- Cooling/Density: liquid; ~8 servers/rack

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000‑based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
