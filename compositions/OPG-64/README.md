# OPG-64 -- Variants Overview

This folder groups assets for 64-xPU training clusters. At this size we keep the
catalog split between compact mesh-converged options and the existing rail-
optimized Clos variant.

Available variants
- mesh-conv-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--inb-2x25g--cooling-air--dens-2srv/
  - What it is: Compact OPG-64 mesh-converged building block with rail-optimized
    scale-out on a DS5000 leaf pair, plus separate `soc-storage`, `inb-mgmt`,
    and `oob-mgmt` fabrics.
  - Why choose it: Minimal switch count while preserving rail-aware scale-out
    semantics and explicit management-fabric separation.
  - Attributes
    - Scale-out: CX7 1x400G per GPU, `rail-optimized`
    - SoC/Storage: BF3 2x200G and storage-facing 2x200G on a two-leaf mesh
    - In-band management: DS2000 with generic 2x25GbE NIC on every server class;
      one port connected
    - OOB management: DS1000 with management/BMC on every device

- mesh-conv-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--inb-2x25g--cooling-air--dens-2srv/
  - What it is: Same mesh-converged OPG-64 building block, but with single-homed
    `same-switch` scale-out instead of rail-optimized scale-out.
  - Why choose it: Operationally simpler scale-out attachment model while keeping
    the remaining fabrics identical to the rail-optimized sibling.
  - Attributes
    - Scale-out: CX7 1x400G per GPU, `same-switch`
    - SoC/Storage: BF3 2x200G and storage-facing 2x200G on a two-leaf mesh
    - In-band management: DS2000 with generic 2x25GbE NIC on every server class;
      one port connected
    - OOB management: DS1000 with management/BMC on every device
  - Consideration
    - Final grouped-per-leaf `same-switch` realization depends on
      `hh-netbox-plugin` issue `#322`

- clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/
  - What it is: Rail-optimized Clos with CX7 1x400G per GPU (RDMA) and BF3
    2x200G for converged frontend.
  - Why choose it: Smooth path to larger OPG tiers using the same wiring rules.

Notes
- Full connection maps and BOMs live inside the relevant variant folder when available.
- The legacy `converged-hyperconverged` path has been replaced by the canonical
  tokenized `mesh-conv-*` variants.
