# Compositions Overview

Welcome. This folder contains the compositions for the Open Cluster Designs aligned AI Training Fabric Reference Architecture.

What is an OPG?
- In OCP’s language, an OPG is a pod‑sized building block: a set of xPU servers, storage/metadata services, and the leaf switches they attach to. If you deploy one OPG, you have a complete small training fabric.

What is an XOC?
- An XOC composes one or more OPGs into a larger cluster, adding the interconnect needed to tie them together. If OPGs are adjacent LEGO bricks, an XOC is how you click them together and add the pieces on top to connect them cleanly.

Why it matters
- OPGs make it easy to size, deploy, and iterate. XOCs let you scale from one OPG to many using the same patterns, with clear trade‑offs.

How this folder is organized
- OPG sizes: `OPG-64`, `OPG-128`, `OPG-256`, `OPG-512`
- XOC tiers: `XOC-256`, `XOC-512`, `XOC-1024` (bundles of OPGs)
- Each size/tier contains one or more variants (e.g., `clos-ro--cx7-1x400g--...` for rail‑optimized Clos). Variant names are tokenized for clarity and grep‑ability.

Assets you’ll find in each variant
- `connectivity-map.csv` — end‑to‑end device/port mapping
- `topology-map.yaml` — authoring plan used to generate inventories and wiring
- `wiring/` — one `wiring-<fabric>.yaml` per Hedgehog‑managed fabric (no OoB files)
- `diagrams/` — draw.io files per fabric
- `netbox_inventory.json` — importable inventory for NetBox

Picking a starting point
- Smaller sites: begin with an OPG (e.g., OPG‑64 or OPG‑128).
- Growing clusters: look at XOC tiers (e.g., XOC‑256 = 2× OPG‑128; XOC‑512 = 4× OPG‑128 or 1× OPG‑512).
- Prefer rail‑optimized variants for training workloads when possible; it can reduce spine traffic and improve job throughput.

Reading the variant names (quick key)
- Topology: `clos-sh` (single‑homed), `clos-ro` (rail‑optimized), `dual-plane` (two independent planes)
- Scale‑out NICs: `cx7-1x400g`, `cx8-2x400g`, `cx9-1x800g`
- Frontend NICs: `bf3-2x200g` (or vendor‑neutral `fe-2x200g`)
- Planes: `1p` or `2p`
- Storage links: `storage-conv-<links>x<speed>` or `storage-ded-<links>x<speed>`
- Cooling: `cooling-air` or `cooling-liquid`
- Density: `dens-<n>srv` (servers per rack)

A note on completeness
- Some large XOC tiers may list partial assets (e.g., topology map only) where scale pushes against current port budgets. Those READMEs call out what’s pending so you can track follow‑ups.

References
- OPG‑M System Architecture (2026‑01‑14): https://www.opencompute.org/documents/opg-m-system-architecture-final-14-january-2026-pdf
- XOC‑N System Architecture (2026‑01‑14): https://www.opencompute.org/documents/xoc-n-system-architecture-final-14-january-2026-pdf

