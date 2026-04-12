# XOC‑512 — 4× OPG‑128

Four OPG‑128 units (16 servers each) are connected behind a shared DS5000 spine layer to
form a 512‑xPU cluster. The XOC spine (DS5000) terminates the 32×800G uplinks from each
OPG's backend rail‑leaf and frontend leaf switches, providing cross‑OPG ECMP and external
egress.

## Variants

- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
  Rail‑optimized backend; air‑cooled; ~2 servers/rack
- [`clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/`](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)
  Rail‑optimized backend; liquid‑cooled; ~8 servers/rack
- [`clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/`](clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)
  Single‑homed backend; air‑cooled; ~2 servers/rack
- [`clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/`](clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)
  Single‑homed backend; liquid‑cooled; ~8 servers/rack

For the sub‑bundle structure see [`2x-OPG-128/`](2x-OPG-128/README.md).

## See also

- XOC‑512 tier overview: [`../../README.md`](../../README.md)
- OPG‑128 building‑block specs: [`../../../OPG-128/`](../../../OPG-128/README.md)
