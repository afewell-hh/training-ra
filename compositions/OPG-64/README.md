# OPG‑64 — Variants Overview

OPG‑64 is a 64‑xPU training building block: 8 compute servers (8 xPUs each) plus the leaf
switches and supporting infrastructure they attach to. It does not include a spine or
external connectivity; those are provided by the XOC when this OPG is composed into a
larger cluster.

## Variants

### collapsed-conv--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/

A single converged DS5000 leaf pair carries both backend (RDMA) and frontend
(storage/in‑band) traffic. No spine is active in this building block; 32×800G uplinks
per leaf are reserved for XOC connectivity or standalone growth. OoB via DS1000.

See [`collapsed-conv--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md`](collapsed-conv--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
for the full building‑block spec including port budget and composer requirements.

### clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/

Rail‑optimized Clos with a separate backend fabric (DS5000 leaf per rail) and a converged
frontend fabric. Each backend rail leaf has 32×800G uplinks reserved for XOC spine
connectivity. Rail‑optimized wiring constrains each CX7 NIC to one rail leaf, producing
predictable switch locality per rail domain.

See [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
for the full building‑block spec.

## Common attributes

- Switch family: DS5000 (800/400/200G) + DS1000 (OoB)
- Port zoning: 4×200G breakouts on odd ports only; 2×400G unrestricted
- Uplink budget: 32×800G per leaf, reserved for XOC spine connectivity
- Frontend multihoming: L3MH/ECMP across two leaves
- Optics: OS2 SMF DR‑class (default)
