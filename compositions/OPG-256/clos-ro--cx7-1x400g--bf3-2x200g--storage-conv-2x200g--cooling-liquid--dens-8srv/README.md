# OPG-256 — Clos Rail-Optimized (CX7 1x400G; BF3 2x200G; Liquid-Cooled; 8 srv/rack)

This composition defines a 256-xPU training cluster (OPG-256) using a rail-optimized two-stage Clos backend fabric and a converged two-stage Clos frontend fabric. Thirty-two GPU servers, each equipped with 8 NVIDIA B200 GPUs and 8 CX7 single-port 400G NICs, are interconnected through 4 backend leaf switches and 4 backend spine switches (all Celestica DS5000). The frontend fabric serves 55 endpoints (32 compute, 10 storage, 10 metadata, 2 gateways, 1 controller) via 2 DS5000 leaf and 2 DS5000 spine switches. Out-of-band management uses 2 Celestica DS1000-48 switches.

This is the liquid-cooled variant at 8 servers per rack (4 racks total). The network topology is identical to the air-cooled variant; only rack density and OOB peripherals (16 PDUs, 4 CDUs) differ. Choose this variant when deploying in a facility with direct liquid cooling (DLC) infrastructure and higher per-rack power density.

## Assets

| File | Description |
|------|-------------|
| `connectivity-map.csv` | Every physical link in the cluster (640 rows): backend, frontend, and OOB |
| `bom.yaml` | Bill of materials: 14 switches, optics (counted at both ends), cables |
| `wiring.yaml` | Rack assignments, port plans, rail mapping, cable types |
| `vpc.yaml` | VPC/VXLAN overlay definitions, underlay eBGP, loopback addressing |
| `diagrams/` | Topology diagrams |

## Attributes

- **Composition:** OPG-256 (32 servers x 8 xPUs = 256 xPUs)
- **Backend:** Rail-optimized Clos; 4 DS5000 leaves, 4 DS5000 spines
- **Frontend:** Converged Clos; 2 DS5000 leaves, 2 DS5000 spines
- **OOB:** 2x DS1000-48 (96 ports >= 76 endpoints)
- **Multihoming:** L3MH (ECMP) on both backend and frontend
- **Port zoning:** DS5000 conventions (E1/1-E1/32 downlinks, E1/33-E1/64 uplinks)
- **Optics:** OS2 single-mode DR-class (800G leaf-spine, 2x400G BE breakout, 4x200G FE breakout)
- **Density:** 8 servers/rack (liquid-cooled) across 4 racks
- **Cooling:** Direct liquid cooling (DLC)

## Considerations

- 16 PDUs (4 per rack); optional 4 CDUs (1 per rack) for coolant distribution monitoring
- 2x DS1000-48 OOB switches provide 96 ports for 76 endpoints (14 spare ports)
- NVIDIA B200/BF3/CX7 used as example xPU/DPU/NIC; the network design is vendor-neutral
- Rail-optimized wiring constrains NIC-to-leaf assignment but uses the same switch count as standard Clos
- All overlay/VPC definitions are identical between air and liquid variants

## References

- OPG-M Building Block Specification (2026-01-14)
- XOC-N Cluster Architecture Specification (2026-01-14)
