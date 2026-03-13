# AI Training Reference Architecture — Assets Repository (Preview Layout)

![OCP](https://img.shields.io/badge/OCP-aligned-blue)
![EVPN/VXLAN](https://img.shields.io/badge/Overlay-EVPN%2FVXLAN-green)
![SONiC](https://img.shields.io/badge/NOS-SONiC-lightgrey)
![Rail‑Optimized](https://img.shields.io/badge/Topology-Rail%E2%80%91Optimized-orange)

Welcome! This repository hosts the open assets that accompany the AI Training Reference Architecture (RA). It’s designed to be easy to browse in the GitHub UI and practical to use in real deployments.

Highlights
- Practical assets per variant: connectivity maps (CSV), BOMs (YAML), Hedgehog CRDs (wiring.yaml, vpc.yaml), and diagrams (SVG/PNG).
- Tokenized variant naming for quick grep/scripting across sizes and options.
- Rail‑optimized guidance to dramatically reduce spine traffic via placement in first‑hop rail domains.
- Clear XOC composition mapping (e.g., XOC‑256 = 2× OPG‑128; XOC‑512 = 4× OPG‑128 or 1× OPG‑512), with folders aligned to bundles.
- Vendor‑neutral, OCP‑aligned wording intended to be directly actionable.

Why this matters
- These assets are intended to be directly useful: you can study the topology, adapt the BOM, and apply CRDs with Hedgehog to realize the described networks. We aim for helpful, educational, OSS‑appropriate guidance rather than product pitch.

Quick navigation
- Catalog index: see `../../docs/catalog.md`
- OPG-64 — see `compositions/OPG-64/README.md`
- OPG-128 — see `compositions/OPG-128/README.md`
- OPG-256 — see `compositions/OPG-256/README.md`
- OPG-512 — see `compositions/OPG-512/README.md`
- XOC-256 — see `compositions/XOC-256/README.md`
- XOC-512 — see `compositions/XOC-512/README.md`
- XOC-1024 — see `compositions/XOC-1024/README.md`

What’s inside (diagram)
- See `compositions/OPG-128/diagrams/README.md` for how diagrams map to CSV IDs. A top‑level overview diagram will be added in a future update.

Status
- This is a modeled structure; assets are placeholders and will be populated. Variant folders include README overviews and placeholder notes until CSV/BOM/CRD/diagrams are added.

Quick start
- Pick a size above and open the composition README.
- Choose a variant (folder) and read its README for attributes and notes.
- Use the assets inside the variant folder:
  - connectivity-map.csv — end‑to‑end cabling and ports
  - bom.yaml — bill of materials (switches, optics, cables)
  - wiring.yaml — Hedgehog Wiring CRDs (Switch, Server, Connection)
  - vpc.yaml — Hedgehog VPC CRDs (VPC, VPCAttachment, External)
- Apply CRDs in a test lab to validate: `kubectl apply -f wiring.yaml && kubectl apply -f vpc.yaml`
- Adapt CSV/BOM to your constraints; keep token naming for traceability.

References
- OPG‑M System Architecture (2026‑01‑14): https://www.opencompute.org/documents/opg-m-system-architecture-final-14-january-2026-pdf
- XOC‑N System Architecture (2026‑01‑14): https://www.opencompute.org/documents/xoc-n-system-architecture-final-14-january-2026-pdf

Rail‑Optimized Benefits (Guidance)
- What it is: A wiring allocation that keeps all NICs of a given rail index on the same leaf (or contiguous leaves at larger scale). It does not change switch counts or oversubscription vs standard Clos.
- Why it matters: When tenants are scheduled within a common first‑hop rail domain, most scale‑out traffic remains leaf‑local, dramatically reducing spine traffic. Since uplink/spine congestion drives most AI network performance issues, this materially improves tail latency and overall job throughput at any scale.
- Scheduling and tenancy: Treat each “first‑hop rail domain” (servers whose rail‑n NICs land on a common leaf) as a preferred placement unit. Packing tenants inside a domain minimizes cross‑spine flows; spreading a tenant across domains forces 100% of scale‑out through the spine.
- Example (composition): In a service built from XOC‑256 as 4× OPG‑64, a 4‑node tenant placed inside a single first‑hop rail domain contributes little spine traffic; the same tenant spread one node per domain across the four OPG‑64s forces all scale‑out via the spine shared by the full composition.
- Leaf radix example (DS5000 51T): 128×400G ports per leaf; with ~50% reserved for uplinks, 64 downlinks remain. With 1×400G per xPU (common for B200/MI300X), up to 64 hosts (512 xPUs) can have their rail‑n NICs terminate on common leaves, enabling substantial spine bypass when scheduling aligns.
- Playbook: Prefer rail‑optimized for training clusters; align tenancy to first‑hop rail domains; use QoS/ECN/PFC to protect remaining FE and control traffic. This is a complementary path alongside protocol and scheduler advances and delivers immediate, durable benefits.
