# OPG‑128 — Variants Overview

OPG‑128 is a 128‑xPU training building block: 16 compute servers (8 xPUs each) plus
dedicated backend and frontend leaf‑spine fabrics. It does not include an XOC spine or
external connectivity; those are supplied when this OPG is composed into an XOC cluster.

## Variants

### Rail‑optimized backend

Each GPU's CX7 1×400G NIC connects to a dedicated backend rail leaf (one NIC per rail).
The wiring pattern constrains NIC‑to‑leaf assignment by rail number, keeping intra‑rail
connections on a single leaf. Each backend rail leaf reserves 32×800G uplinks (ports
33–64) for XOC spine connectivity.

- **[clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)**
  Air‑cooled; ~2 servers/rack
- **[clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/](clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)**
  Liquid‑cooled; ~8 servers/rack

See each variant README for port budget, constraints, and composer requirements.

### Single‑homed backend

Each server's backend NICs terminate on a single leaf (8 servers per leaf). Backend leaves
reserve the same 32×800G uplink budget as rail‑optimized.

- **[clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/](clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/README.md)**
  Air‑cooled; ~2 servers/rack
- **[clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/](clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/README.md)**
  Liquid‑cooled; ~8 servers/rack

### Comparing building‑block patterns

| | Rail‑optimized | Single‑homed |
|--|---------------|--------------|
| NIC‑to‑leaf assignment | By rail number (predictable per GPU) | By server (each server on one leaf) |
| Intra‑rail locality | All GPUs on rail N share a leaf | Varies by server assignment |
| Backend leaf count | One per rail (8 leaves for 8 rails) | One per server group (2 leaves for 16 servers) |
| Uplink budget | 32×800G per rail leaf | 32×800G per backend leaf |

## Common attributes

- Backend switches: DS5000 leaf + DS5000 spine (per fabric)
- Frontend: DS5000 leaf pair (L3MH/ECMP) + DS5000 spine; converged storage/in‑band
- OoB: DS1000
- Port zoning: 4×200G on odd ports; 2×400G unrestricted; 32×800G uplinks per leaf reserved
- Optics: OS2 SMF DR‑class (default)

## Legacy folders

`clos-rail-optimized/` and `clos-single-homed/` are kept for discoverability. Use the
tokenized canonical variants above for all assets and generation.
