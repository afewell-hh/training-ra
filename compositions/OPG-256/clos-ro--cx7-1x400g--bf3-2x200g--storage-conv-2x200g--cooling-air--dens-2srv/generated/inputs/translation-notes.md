# Translation Notes: training-opg256-clos-ro-air-2srv

## Variant Summary

OPG-256 training cluster, rail-optimized Clos backend, air-cooled, ~2 servers/rack.
32 compute servers × 8 xPUs = 256 xPUs total.

## What Was Translated

- Server class: 32 compute servers, 8 GPUs each
- Backend NICs: 8 × CX7 1x400G per server (nic_cx7_single_400)
- Frontend NIC: 1 × BF3 2x200G per server (nic_bf3_2x200)
- Frontend fabric: L3MH across 2 FE leaves (converged frontend)
- Backend fabric: single managed `backend` fabric, rail-optimized, 8 rails

## HNP Switch Count Calculation

HNP calculated: be-rail-leaf=4, fe-leaf=2, be-spine=2, fe-spine=1

This matches the OPG-256 RA description: 4 backend leaves with 2 rails per leaf.
The RA switch summary (4 BE leaves, 4 BE spines) differs slightly from HNP output
(2 BE spines calculated). HNP calculation is authoritative; RA switch counts are
not copied into the plan.

## Frontend Wiring Export Gap

Same pre-existing DIET gap as other variants: frontend wiring YAML export failed with:
  "Switch references group 'fe-mclag' but no PlanMCLAGDomain exists"

Backend wiring exported, validated, and diagrammed successfully.

## Excluded Inputs

Non-compute endpoint counts (storage: 10 per README, metadata: 10 per README,
gateways: 2 per README, controllers: 1) were NOT included in this fixture.
These are mentioned in the OPG-256 RO README but the issue rules for this pipeline
direct compute-only fixture authoring for unconfirmed non-compute counts.

## Generated Counts (HNP)

- Devices: 41
- Interfaces: 704
- Cables: 512
- Switch counts: be-rail-leaf=4, fe-leaf=2, be-spine=2, fe-spine=1
