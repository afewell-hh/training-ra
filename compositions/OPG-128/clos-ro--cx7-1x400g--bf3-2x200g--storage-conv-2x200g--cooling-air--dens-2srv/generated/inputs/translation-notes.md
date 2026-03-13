# Translation Notes

- Pilot scope is compute-only. Storage, controller, gateway, border, and OOB counts are not asserted because the current RA source files do not state them explicitly.
- Switch quantities are HNP-calculated from the topology plan. No README-estimated switch counts were copied into the plan.
- Managed fabrics in this pilot are provisional `frontend` and `backend`.
- Frontend redundancy metadata uses a temporary `mclag` shim solely to satisfy current DIET-side alternating-connection validation. The intended topology semantics are still unbundled L3 multi-homed links, not MCLAG bundles.
- `hhfab validate` succeeds for the backend fabric and fails for the frontend fabric because the DS5000 Hedgehog profile currently rejects both ESLAG and MCLAG semantics. This is a known fast-follow issue for semantic-correct frontend export/validation.
- Because frontend validation fails, only the backend Draw.io diagram is included in this pilot bundle.
