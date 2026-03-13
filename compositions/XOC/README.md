# XOC — Variants Overview

This folder groups assets for cluster‑level compositions made by composing multiple OPGs behind a spine layer.

Tiers and bundles
- XOC-256/
  - 1x-OPG-128/ — one OPG‑128 (useful for demonstrating XOC structure; variants mirror OPG‑128)
- XOC-512/
  - 1x-OPG-512/ — single OPG‑512; variants: rail‑optimized and dual‑plane
  - 2x-OPG-128/ — two OPG‑128 units under a spine; variants: rail‑optimized and single‑homed
- XOC-1024/
  - 2x-OPG-512/ — two OPG‑512 units under a spine; variants: rail‑optimized and dual‑plane

Notes
- Keep tenant placement local to an OPG whenever possible; it reduces spine traffic and aligns with XOC‑N guidance.
- See each tier folder for bundle‑specific READMEs and variant links.
