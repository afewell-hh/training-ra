# XOC‑256 / 2× OPG‑128 — Rail‑Optimized Clos (Liquid)

Overview
- Two OPG‑128 building blocks under an XOC spine layer. Rail‑optimized backend reduces spine load; liquid cooling enables higher rack density.

Why choose it
- Predictable scale with reduced spine congestion and higher density when liquid cooling is available.

Attributes
- Backend: rail‑optimized; CX7 1×400G per GPU
- Frontend: BF3 2×200G per server (L3MH)
- Cooling/Density: liquid; ~8 servers/rack

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
