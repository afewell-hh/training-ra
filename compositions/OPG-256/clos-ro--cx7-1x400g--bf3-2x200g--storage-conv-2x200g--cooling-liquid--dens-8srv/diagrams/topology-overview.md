# OPG-256 Topology Overview — Liquid-Cooled Variant

Network topology is identical to the air-cooled variant. Cooling modality affects only
rack density (8 srv/rack vs 4 srv/rack) and OOB peripheral counts.

```
 ┌─────────────────────────────────────────────────────────────────────────────────┐
 │                        BACKEND FABRIC (Rail-Optimized)                         │
 │                                                                                │
 │        be-spine-01       be-spine-02       be-spine-03       be-spine-04        │
 │        (DS5000)          (DS5000)          (DS5000)          (DS5000)           │
 │           │                  │                 │                  │             │
 │           │    32×800G per leaf-spine pair (8 links to each spine)              │
 │           │                  │                 │                  │             │
 │     ┌─────┼──────────┬──────┼─────────┬───────┼──────────┬───────┼─────┐       │
 │     │     │          │      │         │       │          │       │     │       │
 │  be-leaf-01       be-leaf-02       be-leaf-03       be-leaf-04                 │
 │  (DS5000)         (DS5000)         (DS5000)         (DS5000)                   │
 │  Rails 1,2        Rails 3,4        Rails 5,6        Rails 7,8                  │
 │  E1/1-32          E1/1-32          E1/1-32          E1/1-32                    │
 │  2×400G brk       2×400G brk       2×400G brk       2×400G brk                │
 │     │                 │                │                 │                      │
 │  64×400G           64×400G          64×400G           64×400G                  │
 │  (32 srv×2)        (32 srv×2)       (32 srv×2)        (32 srv×2)              │
 │     │                 │                │                 │                      │
 │  ┌──┴──┐           ┌──┴──┐          ┌──┴──┐           ┌──┴──┐                  │
 │  │NIC  │           │NIC  │          │NIC  │           │NIC  │                  │
 │  │1, 2 │           │3, 4 │          │5, 6 │           │7, 8 │                  │
 │  └──┬──┘           └──┬──┘          └──┬──┘           └──┬──┘                  │
 │     └──────────────────┴────────────────┴──────────────────┘                    │
 │                    32 Compute Servers (compute-01..32)                          │
 │                    8× CX7 400G NICs each = 256 total                           │
 │                                                                                │
 │  + controller-be: 2×400G to be-leaf-01, be-leaf-02                             │
 └─────────────────────────────────────────────────────────────────────────────────┘


 ┌─────────────────────────────────────────────────────────────────────────────────┐
 │                        FRONTEND FABRIC (Converged)                             │
 │                                                                                │
 │              fe-spine-01 (DS5000)       fe-spine-02 (DS5000)                   │
 │                    │                          │                                │
 │                    │    32×800G per leaf-spine pair                             │
 │                    │    (16 links to each spine)                                │
 │              ┌─────┼──────────────────┬───────┼─────┐                          │
 │              │     │                  │       │     │                          │
 │          fe-leaf-01 (DS5000)      fe-leaf-02 (DS5000)                          │
 │          14 odd ports             14 odd ports                                 │
 │          4×200G breakout          4×200G breakout                              │
 │          55 endpoints             55 endpoints                                 │
 │              │                        │                                        │
 │              │         L3MH           │                                        │
 │              │    (ECMP alternating)  │                                        │
 │              │         │              │                                        │
 │           bf3-p1 ──────┘──────── bf3-p2                                        │
 │                                                                                │
 │  55 Endpoints:                                                                 │
 │    32 compute (compute-01..32)     × 2×200G BF3                                │
 │    10 storage (storage-01..10)     × 2×200G BF3                                │
 │    10 metadata (metadata-01..10)   × 2×200G BF3                                │
 │     2 gateways (gateway-01..02)    × 2×200G BF3                                │
 │     1 controller (controller-fe)   × 2×200G BF3                                │
 │  ─────────────────────────────────────────                                     │
 │    55 endpoints × 2 links = 110 total FE links                                 │
 └─────────────────────────────────────────────────────────────────────────────────┘


 ┌─────────────────────────────────────────────────────────────────────────────────┐
 │                    OUT-OF-BAND MANAGEMENT (Liquid Variant)                      │
 │                                                                                │
 │      oob-sw-01 (DS1000-48)  ◄──10G──►  oob-sw-02 (DS1000-48)                  │
 │          │                                    │                                │
 │          │  10G uplink                        │  10G uplink                     │
 │          ▼                                    ▼                                │
 │     Site Management Network                                                    │
 │                                                                                │
 │  OOB Endpoints (76 devices):                                                   │
 │    32 compute BMC ──── bmc0 ──── 1G Cat6a                                      │
 │    10 storage BMC ──── bmc0 ──── 1G Cat6a                                      │
 │    10 metadata BMC ─── bmc0 ──── 1G Cat6a                                      │
 │     2 gateway BMC ──── bmc0 ──── 1G Cat6a                                      │
 │     1 controller-fe BMC ─ bmc0 ── 1G Cat6a                                     │
 │     1 controller-be BMC ─ bmc0 ── 1G Cat6a                                     │
 │    16 PDUs ──────────── mgmt0 ── 1G Cat6a   (4 racks × 4 PDUs)                 │
 │     4 CDUs ──────────── mgmt0 ── 1G Cat6a   (4 racks × 1 CDU, optional)        │
 │  ──────────────────────────────────────────                                    │
 │    76 devices across 2 × 48-port switches = 96 ports (14 spare)                │
 └─────────────────────────────────────────────────────────────────────────────────┘


 ┌─────────────────────────────────────────────────────────────────────────────────┐
 │                         RACK LAYOUT (Liquid-Cooled)                             │
 │                                                                                │
 │   Rack 1              Rack 2              Rack 3              Rack 4           │
 │  ┌──────────┐        ┌──────────┐        ┌──────────┐        ┌──────────┐      │
 │  │compute-01│        │compute-09│        │compute-17│        │compute-25│      │
 │  │compute-02│        │compute-10│        │compute-18│        │compute-26│      │
 │  │compute-03│        │compute-11│        │compute-19│        │compute-27│      │
 │  │compute-04│        │compute-12│        │compute-20│        │compute-28│      │
 │  │compute-05│        │compute-13│        │compute-21│        │compute-29│      │
 │  │compute-06│        │compute-14│        │compute-22│        │compute-30│      │
 │  │compute-07│        │compute-15│        │compute-23│        │compute-31│      │
 │  │compute-08│        │compute-16│        │compute-24│        │compute-32│      │
 │  │──────────│        │──────────│        │──────────│        │──────────│      │
 │  │be-leaf-01│        │be-leaf-02│        │be-leaf-03│        │be-leaf-04│      │
 │  │be-spine-01        │be-spine-02        │be-spine-03        │be-spine-04      │
 │  │fe-leaf-01│        │fe-leaf-02│        │fe-spine-01        │fe-spine-02      │
 │  │oob-sw-01 │        │oob-sw-02 │        │infra svrs│        │infra svrs│      │
 │  │──────────│        │──────────│        │──────────│        │──────────│      │
 │  │4 PDUs    │        │4 PDUs    │        │4 PDUs    │        │4 PDUs    │      │
 │  │1 CDU     │        │1 CDU     │        │1 CDU     │        │1 CDU     │      │
 │  └──────────┘        └──────────┘        └──────────┘        └──────────┘      │
 │                                                                                │
 │  8 srv/rack × 4 racks = 32 GPU servers                                         │
 │  14 switches distributed across racks                                          │
 └─────────────────────────────────────────────────────────────────────────────────┘


 LINK COUNT SUMMARY
 ──────────────────────────────────────────────
  Backend leaf-spine:    128 links (800G)
  Backend server-leaf:   256 links (400G)
  Backend controller:      2 links (400G)
  Frontend leaf-spine:    64 links (800G)
  Frontend endpoint:     110 links (200G)
  OOB devices:            76 links (1G)
  OOB inter-switch:        2 links (10G)
  OOB uplinks:             2 links (10G)
 ──────────────────────────────────────────────
  TOTAL:                 640 links
```
