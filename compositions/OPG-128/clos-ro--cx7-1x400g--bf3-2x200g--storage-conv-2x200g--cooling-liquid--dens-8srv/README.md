# OPG‑128 — Rail‑Optimized Clos (CX7 1×400G, BF3 2×200G, Converged Storage, Liquid, 8 srv/rack)

Liquid‑cooled, higher‑density variant of the rail‑optimized Clos for OPG‑128. When multi‑node jobs are packed within a first‑hop rail domain, scale‑out traffic remains largely leaf‑local, materially reducing spine utilization; networking matches the air‑cooled option.

Attributes
- Backend: single plane, rail‑optimized
- Scale‑out NICs: CX7 1×400G per GPU
- Frontend NICs: BF3 2×200G per server (L3MH)
- Storage: converged, 2×200G per server
- Cooling/Density: liquid‑cooled; ~8 servers/rack (placeholder)
- Optics: OS2 SMF DR‑class (default)
- DS5000 zoning: 4×200G on odd ports; 2×400G unrestricted; 32×800G uplinks/reserved

Assets (placeholders; to be populated)
- connectivity-map.csv, bom.yaml, wiring.yaml, vpc.yaml, diagrams/

Related plans/notes
