# OPG‑128 — Variants Overview

This folder groups assets for the 128‑xPU training composition. We provide two network variants to align with OPG‑M exemplars and common operator preferences.

Variants
- clos-single-homed/
  - What it is: Matches the OPG‑M exemplar where 16 servers are single‑homed on the back‑end — 8 servers to Leaf A, 8 to Leaf B. Frontend is converged and multi‑homed.
  - Why choose it: Clear failure isolation for maintenance (an outage on one leaf impacts only its attached 8 servers); aligns tightly with the OCP paper.
  - Considerations: Cross‑leaf traffic traverses the spine, which can add congestion under load depending on scheduling.

- clos-rail-optimized/
  - What it is: Multi‑homed back‑end (L3MH) with 4×400G per leaf per server to reduce cross‑rail traffic; frontend is identical to the single‑homed variant.
  - Why choose it: All hosts remain available at ~50% capacity during a leaf failure; when tenants are placed within a common first‑hop rail domain, most scale‑out exchanges remain leaf‑local, dramatically reducing spine traffic and associated congestion.
  - Considerations: Benefits are strongest when scheduling keeps tenants inside an OPG.

Common attributes
- DS5000 for 800/400/200G networks; DS3000 optional for border/ISP; DS2000 for in‑band (often single); DS1000 for OoB.
- Port zoning: 4×200G on odd ports; 2×400G unrestricted; 32×800G uplinks per leaf reserved.
- Optics: OS2 single‑mode DR‑class (default); distance‑friendly baseline.

Notes
- Full connectivity maps/BOMs live in each variant folder.

Tokenized variants (canonical for asset generation)
- clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/
  - Rail‑optimized Clos, CX7 1×400G per GPU, BF3 2×200G frontend, converged storage, air‑cooled; density ~2 servers/rack.
- clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/
  - Same topology with liquid‑cooled higher density (~8 servers/rack).
- clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/
  - Single‑homed Clos backend; air‑cooled, ~2 servers/rack.
- clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/
  - Single‑homed backend; liquid‑cooled, ~8 servers/rack.

Legacy note: The two folders above are legacy, kept for discoverability; see canonical tokenized variants below for asset generation.
- Legacy folder names (clos-single-homed/clos-rail-optimized) are maintained with pointers to the canonical tokenized folders.
  We highlight DS5000 here; HH supports 26T designs if desired.
