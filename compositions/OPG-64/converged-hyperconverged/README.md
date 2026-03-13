# OPG‑64 — Converged Hyperconverged

Small/edge OPG with 8 servers × 8 xPUs on a converged DS5000 leaf pair. Frontend (SO‑C/Storage/In‑band) and backend share the same switch pair with L3MH multihoming. OoB via DS1000.

Assets (to be added):
- connectivity-map.csv
- bom.yaml
- wiring.yaml
- vpc.yaml
- diagrams/

Notes
- 4×200G breakouts on odd ports only; 2×400G unrestricted; 32 × 800G uplinks reserved per leaf.

