# Open Cluster Designs Aligned AI Training Fabric Reference Architecture

Badges
- OCP aligned
- EVPN/VXLAN overlay
- SONiC underlay
- Rail‑optimized topology option

Welcome. This repository hosts the open assets for the AI Training Fabric Reference Architecture jointly submitted to the Open Compute Project by Hedgehog and Celestica. Our goal is to make OCP’s Open Cluster Designs approachable and useful to busy operators, architects, and leaders.

About the Open Compute Project (OCP)
- OCP is an industry community that publishes open designs and best practices for data center hardware and infrastructure. Contributions are reviewed in the open and built to be vendor‑neutral and reusable.

Open Systems for AI (OSAI) — why it matters
- OSAI is an OCP strategic initiative focused on practical, interoperable building blocks for AI infrastructure. The vision: make it easier to plan, scale, and operate AI clusters with open designs and shared language. Benefits for operators include clearer choices, lower integration risk, and the ability to evolve hardware without rewriting the architecture.

Open Cluster Designs — OPGs and XOCs in plain terms
- OPG (per OCP’s OPG‑M paper): Think “pod‑sized building block.” It groups a set of xPU servers, storage, and services with the leaf switches they connect to. If you deploy one OPG, you have a small, self‑contained training fabric.
- XOC (per OCP’s XOC‑N paper): Think “one or more OPGs bundled together.” Like clicking LEGO bricks side by side, then adding the pieces needed to link them. XOCs describe how multiple OPGs are interconnected and operated as a larger cluster.
- Why you should care: OPGs make sizing and growth predictable. XOCs let you scale from one OPG to many using the same patterns.

What’s in this repo
- Composition assets you can browse and reuse:
  - connectivity-map.csv — end‑to‑end device/port mapping
  - topology-map.yaml — authoring plan used to generate inventories and wiring
  - wiring/ — one wiring‑<fabric>.yaml per Hedgehog‑managed fabric (no OoB files)
  - diagrams/ — draw.io files per fabric
  - netbox_inventory.json — importable inventory for NetBox
- Compositions are organized by size:
  - OPG‑64, OPG‑128, OPG‑256, OPG‑512 (single building blocks)
  - XOC‑256, XOC‑512, XOC‑1024 (bundles of OPGs)

How to navigate
- Start in `compositions/` for a friendly overview and links to each size.
- Inside a size folder, pick a variant (e.g., rail‑optimized vs single‑homed) and open its README.
- Each variant folder contains the assets listed above. Some larger XOCs may be partially populated where scale pushes against current port budgets; those READMEs call out what’s pending.

Who is this for
- Practitioners who want realistic topologies and inventories.
- Technical leaders who want the “what/why” without wading through dense specs.

References
- OPG‑M System Architecture (2026‑01‑14): https://www.opencompute.org/documents/opg-m-system-architecture-final-14-january-2026-pdf
- XOC‑N System Architecture (2026‑01‑14): https://www.opencompute.org/documents/xoc-n-system-architecture-final-14-january-2026-pdf

Notes on rail‑optimized option
- Rail‑optimized wiring keeps each NIC “rail” localized to a leaf, reducing spine traffic for common training patterns. It complements standard Clos designs and can improve tail latency and throughput when scheduling aligns with rail domains.
