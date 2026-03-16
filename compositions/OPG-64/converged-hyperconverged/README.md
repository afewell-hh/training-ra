# OPG‑64 — Converged Hyperconverged

Small/edge OPG with 8 servers × 8 xPUs on a converged DS5000 leaf pair. Frontend (SO‑C/Storage/In‑band) and backend share the same switch pair with L3MH multihoming. OoB via DS1000.

Assets
- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — HNP topology plan input (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
- 4×200G breakouts on odd ports only; 2×400G unrestricted; 32 × 800G uplinks reserved per leaf.

