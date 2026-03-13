# OPG‑128 — Rail‑Optimized Clos (CX7 1×400G, BF3 2×200G, Converged Storage, Air, 2 srv/rack)

This variant applies a rail‑optimized Clos to a 128‑xPU training cluster (16 servers × 8 xPUs). Backend traffic uses CX7 1×400G per GPU; frontend/storage use BF3 2×200G per server with L3 multi‑homing.

Why choose it
- Dramatically reduces spine traffic when multi‑node jobs are placed within a common first‑hop rail domain (rail‑n NICs on the same leaf), attacking the root cause of most performance issues (uplink/spine congestion).
- Maintains DS5000 zoning rules for easy expansion to larger tiers.
- Air‑cooled density for conventional racks and PDUs.

Attributes
- Backend: single plane, rail‑optimized
- Scale‑out NICs: CX7 1×400G per GPU
- Frontend NICs: BF3 2×200G per server (L3MH)
- Storage: converged, 2×200G per server
- Cooling/Density: air‑cooled; ~2 servers/rack (placeholder)
- Optics: OS2 SMF DR‑class (default)
- DS5000 zoning: 4×200G on odd ports; 2×400G unrestricted; 32×800G uplinks/reserved

Scheduling note
- Prefer packing tenants within the same first‑hop rail domain; spreading across domains forces scale‑out via the spine.

Assets (placeholders; to be populated)
- connectivity-map.csv, bom.yaml, wiring.yaml, vpc.yaml, diagrams/

Related plans/notes
