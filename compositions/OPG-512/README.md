# OPG‑512 — Variants Overview

This folder groups assets for the 512‑xPU training composition. We publish two backend patterns — rail‑optimized (CX7 1×400G) and dual‑plane (CX8 2×400G) — each in air‑ and liquid‑cooled densities.

Variants
- clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/
- clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/
- dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-air--dens-2srv/
- dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-liquid--dens-8srv/

Common attributes
- Frontend: BF3 2×200G per server (L3MH); storage converged at this tier
- Switches: DS5000 for 800/400/200G; DS3000 optional for border; DS1000 (OoB); DS2000 (in‑band)
- Zoning: 4×200G on odd ports; 2×400G unrestricted; preserve 32×800G uplinks per leaf
- Optics: OS2 single‑mode DR‑class (default)

Notes
