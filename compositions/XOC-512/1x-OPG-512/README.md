# XOC‑512 / 1× OPG‑512 — Bundle Overview

This bundle places a single OPG‑512 unit under an XOC spine layer to form a 512‑xPU
cluster. The XOC spine (DS5000) connects the uplinks from the OPG‑512 backend rail‑leaf
and frontend leaf switches, providing cross‑fabric ECMP and external egress that the
OPG‑512 building block does not supply on its own.

## Variants

- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
  Rail‑optimized backend; air‑cooled; ~2 servers/rack
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)
  Rail‑optimized backend; liquid‑cooled; ~8 servers/rack
- [`dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-air--dens-2srv/`](dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
  Dual‑plane backend (CX8 2×400G); air‑cooled; ~2 servers/rack
- [`dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-liquid--dens-8srv/`](dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)
  Dual‑plane backend (CX8 2×400G); liquid‑cooled; ~8 servers/rack

See each variant folder for the full composed‑solution guide.

## See also

- XOC‑512 tier overview: [`../../README.md`](../../README.md)
- OPG‑512 building‑block specs: [`../../../OPG-512/`](../../../OPG-512/README.md)
