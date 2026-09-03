# Hardware reference assembly

This directory releases a reference CAD assembly for the panoramic UAV platform described in the accompanying paper.

## Contents

- `CAD/panoramic_uav_assembly_v1.step`: AP242 STEP reference assembly, in millimetres.
- `CAD/SHA256SUMS`: integrity checksum for the released STEP file.
- `BOM/reference_components.csv`: observed reference components and release boundaries.
- `SAFETY.md`: required engineering and flight-safety boundaries.

## Scope and limitations

The STEP file is a geometry and assembly-reference release. It is not a certified airframe design, a manufacturing drawing package, a complete bill of materials, or a ready-to-fly build guide. The package does not provide verified fastener specifications, wiring diagrams, motor/propeller selection, battery integration, controller parameters, structural analysis, print orientation, infill, or material qualification.

The assembly contains third-party reference components, including propulsion and electronics placeholders. They are included only to preserve fit and placement context. This release does not grant rights to third-party CAD, trademarks, firmware, or product documentation.

## Reuse

Open the STEP file in a standards-compatible CAD tool, inspect all clearances and interfaces, and redesign or revalidate the assembly for your own camera, propulsion, flight-control, and payload configuration. Do not infer airworthiness or safe operating limits from this reference assembly.

Custom design material released in this directory is licensed under CERN-OHL-S v2.0; see `LICENSE-HARDWARE.md`. The license excludes third-party reference components listed in `BOM/reference_components.csv`.
