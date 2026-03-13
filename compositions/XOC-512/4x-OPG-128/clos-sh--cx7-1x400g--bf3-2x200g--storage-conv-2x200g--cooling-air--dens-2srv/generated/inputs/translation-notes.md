# Translation Notes: training_xoc512_4xopg128_clos_sh_air_2srv

## Pass-1 Status: complete-pass1

## Generation Summary
- Plan ID at generation: 45
- Site slug: xoc512-4x-sh-air
- Device count: 0

## Known Gaps

### Frontend Wiring Export
Frontend wiring YAML export fails with:
  "Switch references group 'fe-mclag' but no PlanMCLAGDomain exists"
This is a pre-existing DIET gap affecting all DS5000 L3MH variants.
Backend wiring exported and validated successfully.





## SH Distribution Shim (if applicable)
Single-homed backend variants use rail-optimized distribution (rails 0-7) as a
structural shim. DIET has no per-server SH distribution; this approximates the
intent. Document deviation in RA notes.

## XOC Composition Note (if applicable)
XOC variants are modeled as a single scaled DIET plan with the combined server
count. Per-OPG-unit composition semantics are not modeled in DIET pass-1.

