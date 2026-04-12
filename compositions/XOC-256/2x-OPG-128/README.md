# XOC‑256 / 2× OPG‑128 — Bundle Overview

This bundle composes two OPG‑128 units under a shared DS5000 spine layer to form a
256‑xPU training cluster. The XOC spine connects the uplinks from each OPG's backend
rail‑leaf switches (backend fabric) and frontend leaf switches (frontend fabric) into a
single converged cluster.

## What the XOC spine adds

Each OPG‑128 backend rail‑leaf reserves 32×800G uplinks per switch for XOC connectivity.
The XOC backend spine (DS5000) terminates these uplinks and provides full‑mesh ECMP
between rail leaves across both OPG‑128 units. The XOC frontend spine provides the
equivalent for the converged frontend fabric.

Without the XOC spine, each OPG‑128 operates as an isolated 128‑xPU cluster. The spine
is what allows cross‑OPG traffic and enables the cluster to appear as a single 256‑xPU
fabric to schedulers and storage.

## Variants

All variants use the same OPG‑128 backend and frontend topology; they differ by backend
wiring pattern (rail‑optimized vs single‑homed) and cooling/density:

- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
  Rail‑optimized backend; air‑cooled; ~2 servers/rack
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)
  Rail‑optimized backend; liquid‑cooled; ~8 servers/rack
- [`clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/`](clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
  Single‑homed backend; air‑cooled; ~2 servers/rack
- [`clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/`](clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)
  Single‑homed backend; liquid‑cooled; ~8 servers/rack

See each variant folder for the full composed‑solution guide including spine topology,
tradeoffs, and deployment guidance.

## See also

- XOC‑256 tier overview: [`../README.md`](../README.md)
- OPG‑128 building‑block specs: [`../../OPG-128/`](../../OPG-128/README.md)
- Compositions overview: [`../../README.md`](../../README.md)
