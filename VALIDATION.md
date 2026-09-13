# Validation of CV2-P1

Native KiCad 7.0.11 was used to load the board, refill both copper zones, and
generate DRC reports. The upstream baseline was checked with refilled zones
for comparison. Full reports are included in `validation/`.

The final board has **zero unconnected pads** and no reported copper-clearance,
copper-edge-clearance, track-width, dangling-track, or dangling-via violations.
This does not mean the whole board is DRC-clean.

## DRC comparison

| KiCad finding | Upstream baseline | Modified board |
| --- | ---: | ---: |
| Solder-mask bridge | 186 | 184 |
| Footprint type mismatch | 59 | 59 |
| Hole clearance | 58 | 58 |
| Library footprint issues | 42 | 42 |
| Silkscreen edge clearance | 4 | 35 |
| Starved thermal | 6 | 5 |
| Library footprint mismatch | 3 | 3 |
| Co-located holes | 2 | 2 |
| **Total DRC findings** | **360** | **388** |
| **Unconnected pads** | **0** | **0** |

The 31 additional silkscreen-clearance warnings arise where the fixing-pin
slots approach or intersect existing footprint silkscreen. Review and trim
that silkscreen before fabrication.

The baseline also contains hole-clearance and solder-mask findings around the
reversible switch/socket footprints, plus footprint metadata and library
findings. Some referenced libraries were not available to the validation
environment. Matching or reduced category counts do not constitute a waiver
of those findings; inspect the exact report locations. No findings have been
hidden through added DRC exclusions for this revision.

## Static source checks

The modified board was parsed and compared with the upstream source:

- All 30 switch centers have 5.0 mm nonplated holes.
- All 30 positions have two correctly located 1.5 × 2.0 mm nonplated slots.
- Electrical pad positions, sizes, layers, and net names are unchanged.
- Component positions are unchanged.
- The project minimum track width is 0.15 mm.

The original board has 85 footprints, 3,070 track segments, 418 vias, and two
copper zones. The modified board has 85 footprints, 3,540 track segments,
415 vias, and two copper zones. Segment counts reflect rerouting and splitting
of paths; they are not an electrical performance measurement.

`validation/static-design-checks.json` records these results and the SHA-256
digest of the final PCB. `SHA256SUMS.txt` records the packaged file hashes.

## Limits

The design has not been fabricated or physically assembled. Switch fit, plate
retention, cap clearance, LED current capacity, and complete keyboard operation
remain untested. ERC, an independent schematic-to-PCB netlist audit, and
manufacturing drill-output review are not included in this validation. The
source comparison confirms preservation of the upstream electrical pad/net
assignments, not the correctness of the original circuit.
