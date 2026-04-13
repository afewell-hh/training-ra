# OPG-64 — Variants Overview

OPG‑64 is a 64‑xPU training building block: 8 compute servers (8 xPUs each) plus the leaf
switches and supporting infrastructure they attach to. It does not include a spine or
external connectivity; those are provided by the XOC when this OPG is composed into a
larger cluster.

The compositions in this repository are designed to work with air or liquid cooling at any
density. Cooling medium and rack density are physical deployment choices that do not affect
the network topology.

## Topology variants

### collapsed-conv

A single converged DS5000 leaf pair carries both backend (RDMA) and frontend
(storage/in‑band) traffic. No spine is active in this building block; 32×800G uplinks
per leaf are reserved for XOC connectivity or standalone growth. OoB via DS1000.

### clos-ro (rail‑optimized)

Rail‑optimized Clos with a separate backend fabric (DS5000 leaf per rail) and a converged
frontend fabric. Each backend rail leaf has 32×800G uplinks reserved for XOC spine
connectivity. Rail‑optimized wiring constrains each CX7 NIC to one rail leaf, producing
predictable switch locality per rail domain.

### mesh-conv-ro (mesh converged, rail‑optimized)

Mesh‑converged building block with rail‑optimized scale‑out on a DS5000 leaf pair.
Explicit fabrics for scale‑out, soc‑storage, in‑band management (DS2000, 2×25G per server),
and OoB management (DS1000). Minimal switch count for this OPG‑64 footprint.

### mesh-conv-sh (mesh converged, single‑homed)

Same mesh‑converged topology as the rail‑optimized variant, but with single‑homed
(same‑switch) scale‑out instead. Simpler NIC‑to‑leaf assignment; remaining fabrics
(soc‑storage, inb‑mgmt, oob‑mgmt) are identical to the rail‑optimized sibling.

## Common attributes

- Switch family: DS5000 (800/400/200G) + DS1000 (OoB)
- Port zoning: 4×200G breakouts on odd ports only; 2×400G unrestricted
- Uplink budget: 32×800G per leaf, reserved for XOC spine connectivity
- Frontend multihoming: L3MH/ECMP across two leaves (Clos variants)
- Optics: OS2 SMF DR‑class (default)

## Notes

- Full connection maps and BOMs live inside each variant folder when available.
