# Translation Notes: training-opg128-clos-sh-air-2srv

## Variant Summary

OPG-128 training cluster, single-homed (SH) Clos backend, air-cooled, ~2 servers/rack.
16 compute servers × 8 xPUs = 128 xPUs total.

## What Was Translated

- Server class: 16 compute servers, 8 GPUs each
- Backend NICs: 8 × CX7 1x400G per server (nic_cx7_single_400)
- Frontend NIC: 1 × BF3 2x200G per server (nic_bf3_2x200)
- Frontend fabric: L3MH across 2 FE leaves (converged frontend)
- Backend fabric: single managed `backend` fabric

## Semantic Gap: SH Backend in DIET

The OPG-128 SH topology means each server's ALL 8 backend NICs are single-homed to
ONE backend leaf (8 servers per leaf × 2 leaves = 16 servers total).

DIET does not have a "per-server single-homed alternating" distribution mode. The
available distribution options are:
- `rail-optimized`: GPU N → dedicated leaf (same leaf for all servers' GPU N)
- `alternating`: round-robin, requires redundancy_type (dual-homing with ESLAG/MCLAG)

**Shim applied:** Used `distribution: rail-optimized` with rails 0-7, same as the
OPG-128 RO variant. This produces 8 per-rail leaf groupings (not per-server groupings).
The resulting wiring YAML assigns each GPU's NIC to its rail's leaf across ALL servers,
not per-server leaf assignment.

The practical effect: HNP calculated 2 backend leaves (matching the RA switch count)
because port capacity math works out identically (128 connections / 64 ports per leaf).
The rail assignment pattern differs from true SH but the switch count is correct.

**Required future work:** A `server-sequential` or `per-server-single-homed` distribution
mode in DIET would correctly capture SH semantics.

## Frontend Wiring Export Gap

Frontend wiring YAML export failed with:
  "Switch references group 'fe-mclag' but no PlanMCLAGDomain exists with that switch_group_name"

This is a known pre-existing DIET gap for L3MH frontend export with DS5000 profiles.
The backend wiring was exported, validated with hhfab, and a drawio diagram was generated.
Frontend wiring is tracked as a DIET fast-follow item.

## Excluded Inputs

Non-compute endpoint counts (storage, metadata, gateways, controllers, OOB) were not
explicitly stated in the OPG-128 SH source README and are excluded from this fixture.

## Generated Counts (HNP)

- Devices: 22
- Interfaces: 416
- Cables: 288
- Switch counts: be-leaf=2, fe-leaf=2, be-spine=1, fe-spine=1
