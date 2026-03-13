# Topology Overview — OPG-256 Rail-Optimized (Air-Cooled)

## Backend Fabric (Rail-Optimized Clos)

```
                           SPINE TIER (4x DS5000, 800G)
              ┌──────────────┬──────────────┬──────────────┐
              │              │              │              │
         be-spine-01    be-spine-02    be-spine-03    be-spine-04
         (32x 800G)     (32x 800G)     (32x 800G)     (32x 800G)
              │              │              │              │
    ┌─────────┼──────────────┼──────────────┼──────────────┼─────────┐
    │         │              │              │              │         │
    │    8x800G ea      8x800G ea     8x800G ea      8x800G ea     │
    │         │              │              │              │         │
    ▼         ▼              ▼              ▼              ▼         ▼

   LEAF TIER (4x DS5000, 2x400G breakout downlinks + 800G uplinks)

  be-leaf-01          be-leaf-02          be-leaf-03          be-leaf-04
  Rails 1,2           Rails 3,4           Rails 5,6           Rails 7,8
  ┌────────────┐      ┌────────────┐      ┌────────────┐      ┌────────────┐
  │ P1-32:     │      │ P1-32:     │      │ P1-32:     │      │ P1-32:     │
  │  2x400G BO │      │  2x400G BO │      │  2x400G BO │      │  2x400G BO │
  │  64 x 400G │      │  64 x 400G │      │  64 x 400G │      │  64 x 400G │
  │ P33: ctrl  │      │ P33: ctrl  │      │ P33-64:    │      │ P33-64:    │
  │ P34-64:    │      │ P34-64:    │      │  32x 800G  │      │  32x 800G  │
  │  31x 800G  │      │  31x 800G  │      │  uplinks   │      │  uplinks   │
  └──────┬─────┘      └──────┬─────┘      └──────┬─────┘      └──────┬─────┘
         │                   │                   │                   │
    ┌────┴────┐         ┌────┴────┐         ┌────┴────┐         ┌────┴────┐
    │ 32 srvs │         │ 32 srvs │         │ 32 srvs │         │ 32 srvs │
    │ NIC1,2  │         │ NIC3,4  │         │ NIC5,6  │         │ NIC7,8  │
    │ @400G   │         │ @400G   │         │ @400G   │         │ @400G   │
    └─────────┘         └─────────┘         └─────────┘         └─────────┘

                    SERVER TIER (32x GPU servers, 8x CX7 each)

  gpu-srv-01 ──── NIC1(R1)→be-leaf-01  NIC2(R2)→be-leaf-01
             ──── NIC3(R3)→be-leaf-02  NIC4(R4)→be-leaf-02
             ──── NIC5(R5)→be-leaf-03  NIC6(R6)→be-leaf-03
             ──── NIC7(R7)→be-leaf-04  NIC8(R8)→be-leaf-04
  ...
  gpu-srv-32 ──── (same rail-to-leaf mapping as above)
```

### Rail-to-Leaf Assignment

| Rail | NIC    | Leaf         | Leaf Port (per server N) |
|------|--------|--------------|--------------------------|
| 1    | cx7-nic1 | be-leaf-01 | E1/N/1                   |
| 2    | cx7-nic2 | be-leaf-01 | E1/N/2                   |
| 3    | cx7-nic3 | be-leaf-02 | E1/N/1                   |
| 4    | cx7-nic4 | be-leaf-02 | E1/N/2                   |
| 5    | cx7-nic5 | be-leaf-03 | E1/N/1                   |
| 6    | cx7-nic6 | be-leaf-03 | E1/N/2                   |
| 7    | cx7-nic7 | be-leaf-04 | E1/N/1                   |
| 8    | cx7-nic8 | be-leaf-04 | E1/N/2                   |

Each physical port on a BE leaf is broken out into 2x400G subports.
Server N uses physical port N on each leaf (E1/N/1 and E1/N/2).


## Frontend Fabric (Converged Clos)

```
                      SPINE TIER (2x DS5000, 800G)
                  ┌────────────────────────────┐
                  │                            │
             fe-spine-01                  fe-spine-02
             (32x 800G leaf               (32x 800G leaf
              + 3x 10G OOB)               + 3x 10G OOB)
                  │                            │
         ┌───────┴────────────────────────┬────┘
         │          16x 800G each         │
         ▼                                ▼

      LEAF TIER (2x DS5000, 4x200G breakout + 800G uplinks)

  fe-leaf-01                          fe-leaf-02
  ┌──────────────────┐                ┌──────────────────┐
  │ Odd P1-27:       │                │ Odd P1-27:       │
  │  14 ports x 4BO  │                │  14 ports x 4BO  │
  │  = 56x 200G      │                │  = 56x 200G      │
  │ P33-64:          │                │ P33-64:          │
  │  32x 800G uplinks│                │  32x 800G uplinks│
  └────────┬─────────┘                └────────┬─────────┘
           │                                   │
      55 endpoints                        55 endpoints
      (1x 200G each)                      (1x 200G each)

                    ENDPOINT TIER (L3MH — 1 link per leaf)

  ┌─────────────────────────────────────────────────────────┐
  │ 32x gpu-srv-NN      bf3-p1 → fe-leaf-01                │
  │                     bf3-p2 → fe-leaf-02                 │
  │ 10x stor-srv-NN     bf3-p1 → fe-leaf-01                │
  │                     bf3-p2 → fe-leaf-02                 │
  │ 10x meta-srv-NN     bf3-p1 → fe-leaf-01                │
  │                     bf3-p2 → fe-leaf-02                 │
  │  2x hh-gw-NN        bf3-p1 → fe-leaf-01                │
  │                     bf3-p2 → fe-leaf-02                 │
  │  1x hh-ctrl-fe      bf3-p1 → fe-leaf-01                │
  │                     bf3-p2 → fe-leaf-02                 │
  │                                                         │
  │ Total: 55 endpoints × 2 links = 110 links              │
  └─────────────────────────────────────────────────────────┘
```

### Frontend Port Assignment (per leaf)

Odd ports with 4x200G breakout, endpoints assigned sequentially:

| Phys Port | Subports  | Endpoints (by index 1-55)       |
|-----------|-----------|---------------------------------|
| E1/1      | /1 to /4  | gpu-srv-01 through gpu-srv-04   |
| E1/3      | /1 to /4  | gpu-srv-05 through gpu-srv-08   |
| E1/5      | /1 to /4  | gpu-srv-09 through gpu-srv-12   |
| E1/7      | /1 to /4  | gpu-srv-13 through gpu-srv-16   |
| E1/9      | /1 to /4  | gpu-srv-17 through gpu-srv-20   |
| E1/11     | /1 to /4  | gpu-srv-21 through gpu-srv-24   |
| E1/13     | /1 to /4  | gpu-srv-25 through gpu-srv-28   |
| E1/15     | /1 to /4  | gpu-srv-29 through gpu-srv-32   |
| E1/17     | /1 to /4  | stor-srv-01 through stor-srv-04 |
| E1/19     | /1 to /4  | stor-srv-05 through stor-srv-08 |
| E1/21     | /1 to /4  | stor-srv-09, stor-srv-10, meta-srv-01, meta-srv-02 |
| E1/23     | /1 to /4  | meta-srv-03 through meta-srv-06 |
| E1/25     | /1 to /4  | meta-srv-07 through meta-srv-10 |
| E1/27     | /1 to /4  | hh-gw-01, hh-gw-02, hh-ctrl-fe, (spare) |


## OOB Fabric

```
                    FE SPINES (OOB peering zone)
              fe-spine-01              fe-spine-02
              E1/65-67 (10G)           E1/65-67 (10G)
                  │                        │
         ┌───────┼────────────────────┬────┘
         │       │    10G SFP+ LR    │
         ▼       ▼                   ▼

      OOB SWITCHES (3x DS1000-48, 1G copper + 10G SFP+ uplinks)

  oob-sw-01              oob-sw-02              oob-sw-03
  ┌──────────────┐       ┌──────────────┐       ┌──────────────┐
  │ E1/1-40:     │       │ E1/1-40:     │       │ E1/1-40:     │
  │  40x 1G      │       │  40x 1G      │       │  40x 1G      │
  │ E1/49-50:    │       │ E1/49-50:    │       │ E1/49-50:    │
  │  2x 10G SFP+ │       │  2x 10G SFP+ │       │  2x 10G SFP+ │
  └──────┬───────┘       └──────┬───────┘       └──────┬───────┘
         │                      │                      │
    40 endpoints           40 endpoints           40 endpoints

  Endpoints (120 total, distributed across 3 switches):
  ├── 32x gpu-srv BMCs          (bmc0)
  ├── 10x stor-srv BMCs         (bmc0)
  ├── 10x meta-srv BMCs         (bmc0)
  ├──  2x gateway BMCs          (bmc0)
  ├──  1x hh-ctrl-fe BMC        (bmc0)
  ├──  1x hh-ctrl-be BMC        (bmc0)
  └── 64x PDUs                  (mgmt0, 4 per rack × 16 racks)
```


## Physical Rack Layout (16 compute racks, air-cooled)

```
  Rack 01    Rack 02    Rack 03   ...   Rack 16
  ┌──────┐   ┌──────┐   ┌──────┐       ┌──────┐
  │srv-01│   │srv-03│   │srv-05│       │srv-31│
  │srv-02│   │srv-04│   │srv-06│       │srv-32│
  │ 4xPDU│   │ 4xPDU│   │ 4xPDU│       │ 4xPDU│
  └──────┘   └──────┘   └──────┘       └──────┘

  2 servers per rack = 16 racks for 32 compute servers
  4 PDUs per rack = 64 PDUs total (managed via OOB)

  Additional racks for switches, storage, metadata, gateways,
  and controllers are site-dependent and not prescribed here.
```


## Link Count Summary

| Connection Type               | Links | Speed | Optic              |
|-------------------------------|-------|-------|--------------------|
| BE leaf-spine                 | 126   | 800G  | OSFP 2x400G DR4   |
| BE leaf-server (rails)        | 256   | 400G  | OSFP 2x400G DR4 (leaf) / QSFP112 400G DR4 (server) |
| BE leaf-controller            | 2     | 400G  | OSFP 2x400G DR4 (leaf) / QSFP112 400G DR4 (ctrl) |
| FE leaf-spine                 | 64    | 800G  | OSFP 2x400G DR4   |
| FE leaf-endpoint              | 110   | 200G  | OSFP 4x200G DR4 (leaf) / QSFP56 200G DR4 (server) |
| OOB switch-endpoint           | 120   | 1G    | Cat6a copper       |
| OOB switch-spine uplink       | 6     | 10G   | SFP+ 10G LR       |
| **Total**                     | **684** |     |                    |
