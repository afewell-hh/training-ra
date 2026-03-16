Title: Ticket — Variant Naming Taxonomy (OPG/XOC)
Owner: strategy@hedgehog.cloud
Status: Open

Objective
- Propose a clear, scalable naming convention for OPG/XOC variants that captures topology pattern, hardware generation, NIC speeds, and plane count, while remaining concise and reviewer‑friendly.

Inputs/Constraints
- OPG‑M uses terms like “single‑homed” and “rail‑optimized”; XOC‑N focuses on composition. There is no canonical compact code today.
- We need names that work in folder paths, READMEs, and RA prose.

Deliverable
- A short RFC (1–2 pages) with recommended patterns, examples, and mapping rules.

Proposal v1.1 (adds density and storage flags)
- Goals: concise, human‑parsable, future‑proof; compatible with folder names; aligns with OCP terms.
- Folder token format (ordered):
  <topo>--<so>--<fe>[--<planes>][--<storage>][--<cooling>][--<density>]
  - topo: clos-sh (Clos single-homed), clos-ro (Clos rail-optimized), dual-plane (for scale-out)
  - so (scale-out NICs): cx7-1x400g, cx8-2x400g, cx9-1x800g (pattern: <model>-<ports>x<speed>)
  - fe (frontend NICs): bf3-2x200g (or fe-2x200g for vendor-neutral)
  - planes: 1p or 2p (defaults: clos-sh/ro = 1p; dual-plane = 2p)
  - storage: storage-conv-<links>x<speed> or storage-ded-<links>x<speed>
    - Examples: storage-conv-2x200g (frontend converged SO‑C/Storage 2×200G)
               storage-ded-2x100g (dedicated storage fabric 2×100G)
  - cooling: cooling-air or cooling-liquid (cooling type; orthogonal to density)
  - density: dens-<n>srv (servers per rack, e.g., dens-2srv, dens-4srv, dens-8srv)

Examples
- OPG-128/clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/
- OPG-128/clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/
- OPG-256/dual-plane--cx8-2x400g--bf3-2x200g--2p--storage-conv-2x200g--cooling-air--dens-2srv/
- Future dedicated storage example:
  OPG-128/clos-ro--cx7-1x400g--bf3-2x200g--storage-ded-2x100g--cooling-air--dens-4srv/

Display name pattern for READMEs
- “Clos Single‑Homed (CX7 1×400G scale‑out; BF3 2×200G frontend; Storage: Converged 2×200G; Cooling: Air; Density: 2 srv/rack)”

XOC variant names
- XOC folders mirror the underlying OPG variant tokens for traceability, prefixed by the composition count:
  - XOC-256/1x-OPG-128-clos-sh--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-air--dens-2srv/
  - XOC-512/2x-OPG-128-clos-ro--cx7-1x400g--bf3-2x200g--storage-conv-2x200g--cooling-liquid--dens-8srv/

Tasks
- Validate with OCP reviewers; adjust tokens if they prefer alternative abbreviations.
- Ensure tokens sort well; document in RA_REPOS/CONTRIBUTING.md after agreement.

Tasks
- Survey OCP precedent for naming (if any) and existing community practice.
- Test readability in folder structures and in RA prose.
- Produce final recommendation with examples for OPG‑64/128/256 and XOC‑256/512.

Acceptance Criteria
- Naming taxonomy is accepted and applied to new folders/variants; guidance added to RA_REPOS/CONTRIBUTING.md.
