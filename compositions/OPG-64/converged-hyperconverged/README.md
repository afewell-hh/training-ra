# OPG‑64 — Converged Hyperconverged

Overview
- Compact, operator‑friendly building block: 8 servers × 8 xPUs connected to a single DS5000 leaf pair.
- Frontend (SO‑C/Storage/In‑band) and backend share the same leaf pair using L3 multihoming (ECMP). OoB is handled by DS1000.
- Ideal for pilots, edge, or first deployments where simplicity beats absolute peak scale.

Why choose it
- Fewer moving parts: one converged leaf pair to operate and monitor.
- Clear growth path: add another OPG or step up to XOC tiers without re‑thinking the basics.
- Friendly failure domains: small blast radius and straightforward troubleshooting.

Attributes
- Backend: converged on DS5000 leaf pair (single plane)
- Multihoming: L3MH/ECMP
- NICs: CX7 1×400G per GPU (backend); BF3 2×200G per server (frontend/storage)
- Zoning: 4×200G on odd ports; 2×400G unrestricted; 32×800G uplinks reserved per leaf
- Optics: OS2 SMF DR‑class defaults

How to use
- Browse assets below, import `netbox_inventory.json` if you use NetBox, review `diagrams/`, then apply wiring/VPC CRDs with Hedgehog in a lab.
- Keep tenant placement simple: co‑locate nodes for a job to minimize leaf‑to‑leaf flows.

Assets
- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000‑based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

Notes
- 4×200G breakouts on odd ports only; 2×400G unrestricted; 32×800G uplinks reserved per leaf.

See also
- Size overview: ../README.md
- Compositions overview: ../../README.md
