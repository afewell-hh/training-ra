# Translation Notes: training_opg128_clos_ro_liquid_8srv

## Pass-1 Status: complete-pass1

## Generation Summary
- Plan ID at generation: 55
- Site slug: opg128-clos-ro-liquid
- Device count: 0

## Known Gaps

### Frontend Wiring Export
Frontend wiring YAML export fails with:
  "Switch references group 'fe-mclag' but no PlanMCLAGDomain exists"
This is a pre-existing DIET gap affecting all DS5000 L3MH variants.
Backend wiring exported and validated successfully.



### Liquid Cooling Variant
This variant is topologically identical to the corresponding air-cooled variant.
Cooling medium and rack density differ only (not modeled in DIET).
Reference air-cooled variant for the same wiring topology.

## SH Distribution Shim (if applicable)
Single-homed backend variants use rail-optimized distribution (rails 0-7) as a
structural shim. DIET has no per-server SH distribution; this approximates the
intent. Document deviation in RA notes.

## XOC Composition Note (if applicable)
XOC variants are modeled as a single scaled DIET plan with the combined server
count. Per-OPG-unit composition semantics are not modeled in DIET pass-1.

