# OPG-256 — Rail-Optimized Clos Building Block (CX7 1×400G; BF3 2×200G; Liquid-Cooled; 8 srv/rack)

This building block provides a 256-xPU rail-optimized Clos network for 32 eight-GPU servers in a liquid-cooled configuration (8 servers per rack, 4 racks). Thirty-two GPU servers, each equipped with 8 NVIDIA B200 GPUs and 8 CX7 single-port 400G NICs, are interconnected through backend leaf switches and backend spine switches (all Celestica DS5000). The frontend fabric serves endpoints via DS5000 leaf and spine switches. Out-of-band management uses Celestica DS1000-48 switches.

The network topology is identical to the air-cooled variant; only rack density and OOB peripherals (16 PDUs, 4 CDUs) differ. This OPG does not include an XOC spine; uplink ports are reserved on each leaf for XOC connectivity.

## Assets

- `connectivity-map.csv` — end-to-end cabling and port mapping
- `topology-map.yaml` — HNP topology plan input (DS5000-based)
- `wiring/` — Hedgehog Wiring CRDs
  - `wiring-backend.yaml` — backend fabric wiring
- `diagrams/` — visual diagrams
  - `hhfab/backend.drawio` — backend topology diagram (draw.io)
- `netbox_inventory.json` — NetBox inventory export

## Attributes

- **Scale:** OPG-256 (32 servers × 8 xPUs = 256 xPUs)
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

## Composer requirements

To form a functional XOC cluster using this OPG, the composer must supply:

1. **XOC backend spine switches** (DS5000): cable to the 32×800G reserved uplinks on each
   backend rail leaf (ports 33–64 per switch)
2. **XOC frontend spine switches** (DS5000): cable to the 32×800G reserved uplinks on each
   frontend leaf (even ports 2–64 per switch)
3. **External/border connectivity** (DS3000 or equivalent) for WAN/ISP uplinks if required

## References

- OPG-M Building Block Specification (2026-01-14)
- XOC-N Cluster Architecture Specification (2026-01-14)
