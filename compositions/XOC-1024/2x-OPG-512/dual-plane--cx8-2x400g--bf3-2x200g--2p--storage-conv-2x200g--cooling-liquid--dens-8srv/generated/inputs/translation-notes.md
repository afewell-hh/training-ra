# Translation Notes: training_xoc1024_2xopg512_dual_plane_liquid_8srv

## Pass-1 Status: needs-fast-follow

## Generation Gap: Port Exhaustion at XOC-1024 Scale

Device generation failed with port exhaustion:
  "Requested 1 ports but only 0 remain in zone 'be-server-ports'"

Root cause: The single-plane clos rail-optimized topology saturates at OPG-512 (64 servers).
- 128 servers × 8 rails → 8 rail-leaf switches
- Each leaf must handle 128 server connections (one per server per rail)
- Port zone 'be-server-ports' (port_spec: 1-32, b_2x400) = 64 logical ports per leaf
- 128 connections > 64 ports → exhausted

OPG-512 is the topology ceiling for this port zone configuration.

## Fast-Follow Actions Required
1. Either expand rails to 16 (would require 16 NICs per server — departs from RA)
2. Or model XOC-1024 as two independent OPG-512 DIET plans (matches XOC composition semantics)
3. The per-OPG-unit composition semantics gap is already documented (XOC pass-1 note)

## XOC Composition Note
XOC-1024 = 2×OPG-512. The correct DIET approach is two separate plans per OPG-512 unit.
Pass-1 attempted single-plan modeling; port exhaustion confirms topology doesn't scale.
Reference: OPG-512 variants in this repo for valid generated assets.
