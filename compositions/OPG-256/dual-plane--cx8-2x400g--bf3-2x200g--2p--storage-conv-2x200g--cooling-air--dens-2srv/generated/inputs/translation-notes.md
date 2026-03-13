# Translation Notes: training-opg256-dual-plane-air-2srv

## Variant Summary

OPG-256 training cluster, dual-plane backend, air-cooled, ~2 servers/rack.
32 compute servers × 8 xPUs = 256 xPUs total. Two independent backend fabrics.

## What Was Translated

- Server class: 32 compute servers, 8 GPUs each
- Backend NICs: 8 × CX8 dual-port 400G per server (nic_cx8_dual_400)
  - port0 → backend-plane-a (rail-optimized, rails 0-7)
  - port1 → backend-plane-b (rail-optimized, rails 0-7)
- Frontend NIC: 1 × BF3 2x200G per server (nic_bf3_2x200)
- Frontend fabric: L3MH across 2 FE leaves
- Backend fabrics: two independent managed fabrics `backend-plane-a` and `backend-plane-b`

## New NIC Module Type

nic_cx8_dual_400 (ConnectX-8 Dual-Port 400G): new module type not in the OPG-128 pilot.
Defined with port0 and port1 interface templates.

## DIET Translation Approach for Dual Plane

Each GPU's CX8 NIC contributes two server_connections:
- port_index 0 → backend-plane-a-leaf (rail N)
- port_index 1 → backend-plane-b-leaf (rail N)

This models each plane as an independent fabric with rail-optimized distribution.
17 connections per server class (1 FE + 8 GPU × 2 planes).

## HNP Switch Count Calculation

HNP calculated:
- be-plane-a-leaf: 4, be-plane-a-spine: 2
- be-plane-b-leaf: 4, be-plane-b-spine: 2
- fe-leaf: 2, fe-spine: 1
Total switches: 15

## Validation Results

- backend-plane-a: hhfab validate PASSED
- backend-plane-b: hhfab validate PASSED
- frontend: NOT exported (pre-existing MCLAG domain gap)

## Excluded Inputs

Non-compute endpoint counts not included (not in source README).

## Generated Counts (HNP)

- Devices: 47
- Interfaces: 2112
- Cables: 896
