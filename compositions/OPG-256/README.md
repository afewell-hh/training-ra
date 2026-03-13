# OPG-256 — Variants Overview

This folder groups assets for the 256-xPU training composition (32 servers × 8 xPUs). Two backend topology patterns are provided, each with air-cooled and liquid-cooled density variants.

## Variants

### Rail-Optimized — B200 Generation (BF3 + CX7 1×400G)

- **clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/**
  Rail-optimized backend with 4 DS5000 leaves (2 rails per leaf). Air-cooled density: 2 servers/rack, 16 racks, 64 PDUs.

- **clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/**
  Same network topology as above. Liquid-cooled density: 8 servers/rack, 4 racks, 16 PDUs + optional CDUs.

**When to choose rail-optimized:** Intra-rail collective traffic (all-reduce, all-gather) stays within a single leaf, reducing spine utilization. At OPG-256, each leaf serves two rails; scheduling jobs aligned to rail pairs further improves locality.

### Dual-Plane — B300 Generation (BF3 + CX8 2×400G)

Two independent backend fabrics (Plane A and Plane B) for increased bandwidth and plane-level serviceability. CX8 NICs provide 2×400G per GPU: port-1 to Plane A, port-2 to Plane B.

- **dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-air--dens-2srv/**
  Dual-plane backend with air-cooled density: 2 servers/rack (placeholder). L3MH on frontend as in rail-optimized variant.

- **dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-liquid--dens-8srv/**
  Same topology; liquid-cooled higher density: 8 servers/rack (placeholder).

## Common Attributes

- **Frontend:** Converged (SO-C/Storage/In-band) with BF3 2×200G per endpoint, L3MH across two DS5000 FE leaves.
- **Switches:** DS5000 for 800/400/200G networks; DS1000-48 for OoB; DS2000 for in-band (optional).
- **Port zoning:** 4×200G on odd ports; 2×400G unrestricted; 32×800G uplinks per leaf.
- **Optics:** OS2 single-mode DR-class (default). Distance-friendly baseline; substitute optics per site survey.

## Notes

- Full connectivity maps, BOMs, and Hedgehog CRDs live in each variant folder.
- NVIDIA B200/B300 and BF3/CX7/CX8 are used as concrete examples; the network design is vendor-neutral for equivalent speeds and link counts.
