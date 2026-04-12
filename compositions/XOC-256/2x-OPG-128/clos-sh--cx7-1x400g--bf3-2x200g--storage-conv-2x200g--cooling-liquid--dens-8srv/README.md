# XOC‑256 / 2× OPG‑128 — Single‑Homed Clos (CX7 1×400G, BF3 2×200G, Liquid, 8 srv/rack)

## Composed topology

Two OPG‑128 building blocks (16 servers each) are connected under a shared DS5000 spine
layer to form a 256‑xPU training cluster. Network topology is identical to the air‑cooled
variant; only rack density and OoB peripherals differ.

**Backend fabric:** Single‑homed — each server's backend NICs terminate on one backend
leaf (8 servers per leaf). Backend leaf uplinks (32×800G per leaf, ports 33–64) connect
to the XOC backend spine (DS5000).

**Frontend fabric:** BF3 2×200G per server, L3MH across two frontend leaves. Frontend
leaf uplinks (32×800G per leaf, even ports 2–64) connect to the XOC frontend spine.

**OoB:** DS1000 per OPG‑128 unit for BMC and PDU management.

## Composition attributes

| Attribute | Value |
|-----------|-------|
| Total xPUs | 256 (32 servers × 8 xPUs) |
| Backend topology | Single‑homed Clos (8 servers per backend leaf) |
| Backend spine | DS5000 (XOC‑level) |
| Frontend topology | 2‑stage Clos (FE leaves + FE spine) |
| Cooling / Density | Liquid; ~8 servers/rack |
| Scale‑out NICs | CX7 1×400G per GPU |
| Frontend NICs | BF3 2×200G per server (L3MH) |

## Why this composition

Same single‑homed topology as the air‑cooled variant; liquid cooling reduces rack count
from ~16 racks to ~4 racks and shortens cable runs. Choose this variant when straightforward
operations, predictable failure isolation, and a compact liquid‑cooled footprint are all
priorities.

## Tradeoffs

- **Single‑homed backend:** any job spanning servers on different backend leaves generates
  cross‑spine traffic; no rail‑domain locality benefit.
- **Liquid‑cooled density:** ~8 servers/rack reduces footprint; requires DLC infrastructure
  (CDUs).
- **DS1000 OoB is per OPG unit.**

## OPG‑128 building blocks

This composition uses two instances of OPG‑128 clos‑sh. For the building‑block spec, see:
`../../../OPG-128/clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md`

## How to use

1. Deploy and validate each OPG‑128 unit independently.
2. Install XOC spine switches (be‑spine and fe‑spine, DS5000).
3. Cable the 32×800G uplinks from each backend leaf to the be‑spine, and the
   32×800G uplinks from each frontend leaf to the fe‑spine.
4. Import `netbox_inventory.json` into NetBox (optional) and apply Hedgehog Wiring CRDs
   from the `wiring/` folder.

## Assets

- `connectivity-map.csv` — end‑to‑end cabling and port mapping
- `topology-map.yaml` — topology authoring plan (DS5000‑based)
- `wiring/` — Hedgehog Wiring CRDs (per fabric)
- `diagrams/` — visuals (per fabric)
- `netbox_inventory.json` — NetBox inventory export

## See also

- Bundle overview: `../README.md`
- OPG‑128 building blocks: `../../../OPG-128/README.md`
- Compositions overview: `../../../README.md`
