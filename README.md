# Sofle Choc Wireless — Choc v2 PCB prototype

Revision: CV2-P1, 2026-09-13. Based on
[db-ok/SofleChocWireless](https://github.com/db-ok/SofleChocWireless/tree/aae7cc0ac5ca563dab8222320ae8749ed1911e56),
commit `aae7cc0ac5ca563dab8222320ae8749ed1911e56`.

This project modifies the reversible Sofle Choc Wireless PCB for Kailh Choc v2
(PG1353) switch mounting. The PCB, three switch footprint definitions, and
minimum track-width constraint have been changed. Nearby traces and vias have
been rerouted around the enlarged holes.

**This is an unbuilt prototype.** Connectivity passes KiCad's check, but the
board still has DRC findings described in `VALIDATION.md`. Review those findings
and test physical fit before ordering an assembled keyboard or a production run.

## AI-Generated Changes Disclosure

The changes in this fork were generated using ChatGPT 6 Astra Max and have not been independently reviewed or tested.

## Open the design

Extract the complete ZIP, then open:

`SofleChocWireless/PCB/SofleKeyboard.kicad_pro`

Use KiCad 7 or newer. The routed board is
`SofleChocWireless/PCB/SofleKeyboard.kicad_pcb`; the schematic is alongside it.
Keep the folder structure so the project-local library paths resolve. Standard
KiCad libraries may be needed to edit or replace other components. Footprints
are embedded in the PCB, including the revised switch geometry.

The source schematic is electrically unchanged. No firmware matrix changes are
required by these mechanical switch changes.

## PCB changes

| Feature | Revised geometry |
| --- | --- |
| Switch center hole | 5.0 mm nonplated hole at each of 30 positions per half |
| Fixing-pin relief | Two mirrored 1.5 × 2.0 mm nonplated slots per switch; 60 total |
| Ordinary switch slot centers | Local coordinates (−5, 5.15) and (5, 5.15) mm |
| Optional encoder-position switch SW25 | Slots at local (−5, −5.15) and (5, −5.15) mm, matching its reversed switch orientation |
| Minimum track width | 0.15 mm, with new route sections using this width |
| Copper clearance constraint | Existing 0.20 mm minimum retained |
| Hole clearance constraint | Existing 0.25 mm minimum retained |

The 3.4 mm switch center holes were enlarged. At the 29 ordinary hotswap
positions, the old small boss holes were replaced by the fixing-pin slots.
SW25 received the two slots as well. Slot orientation follows each footprint,
including the angled thumb switches. Both mirrored positions are included for
the reversible PCB.

Electrical pad positions, sizes, layers, net names, and component positions
match the original board. Routing changes affect nearby matrix, LED, and ground
connections. Copper zones were refilled after rerouting. Ground vias were moved,
added, or removed as needed to retain connectivity around the new holes.

The three updated library footprints are in
`SofleChocWireless/PCB/SofleChoc.pretty/`:

- `Choc_Hotswap_SK6812MiniE_BiggerHSPads.kicad_mod` — 25 placements.
- `Choc_Hotswap_SK6812MiniE_BiggerHSPads_Column1.kicad_mod` — 4 placements.
- `Kailh-PG1350-1u-reversible-SK6812MiniE_MODIFIED.kicad_mod` — SW25.

Their original names are retained so existing schematic and board references
continue to resolve. Other footprint variants in the bundled libraries were
not converted to Choc v2.

## Assembly and fabrication

The original 29 hotswap positions and optional switch/encoder position are
retained. The existing wireless controller, battery, display, encoder, and LED
circuits are retained.

The center-hole and fixing-slot geometry targets PG1353, with slot relief
cross-checked against the PG1353S drawing. Physical compatibility has not been
tested with either variant. Choc v1 fit is also unverified after replacing the
original boss holes.

The case and plate files are included unchanged as reference geometry. Check
plate thickness, switch retention, keycap clearance, and standoff heights
against the exact switch variant and keycaps you intend to use. The existing
plate file settings are not a Choc v2 assembly specification.

Choose a PCB process that supports the project's 0.15 mm traces and routed
nonplated slots. Review the remaining DRC findings, inspect both copper layers
around the switch openings, and regenerate Gerbers and drill files from this
modified board after review. Confirm that the drill output contains the slots.
No fabrication exports are included in this package.

Prototype checks should cover switch seating on both PCB orientations, hotswap
socket clearance, matrix operation, wireless power operation, and LED operation
under the intended load. These have not been physically tested.

## Design references

- [Upstream source and build guide](https://github.com/db-ok/SofleChocWireless/blob/aae7cc0ac5ca563dab8222320ae8749ed1911e56/docs/build_guide_choc_wireless.md).
- [Kailh PG1353 datasheet, archived by Keyboardio](https://github.com/keyboardio/keyswitch_documentation/blob/323ea47b7b90550327231fa311a2762b1308661a/datasheets/Kailh/CPG135301D02.pdf).
- [Kailh PG1353S datasheet](https://www.kailhswitch.com/uploads/15927/files/CPG1353S01D02-01-data-sheet.pdf).
- [ai03 PG1353 hotswap footprint cross-check](https://github.com/ai03-2725/MX_V2/blob/0b379eebbeb66c7fd6e82e400b47958ad695614e/Kailh_PG1353_Hotswap.pretty/Kailh-PG1353-Hotswap-1U.kicad_mod).

The upstream license is included in `LICENSE`.
