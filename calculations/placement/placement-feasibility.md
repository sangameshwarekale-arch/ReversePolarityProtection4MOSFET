# Read-only four-MOSFET placement feasibility study

**Conditional spatial feasibility found. All 24 electronics can be placed on the front inside the fixed polygon, with their existing courtyards and fixed pad keepouts. This is an unrouted starting placement, not a60 A release.** Current duty, cooling, terminations, copper weights and via plating remain unresolved. No PCB was saved or edited by this study.

The saved outline is one valid KiCad polygon tessellated from60 Edge.Cuts primitives. Polygon bounds are104.588766–149.111254mm in X and72.041499–113.550025mm in Y:44.522488×41.508526mm. The 12 locked mechanical footprints are preserved; they define24 fixed plated holes/pads, including the seven isolated balance endpoints on J1. There are36 footprints, two copper layers, zero tracks and zero zones in the source. The fixed footprints contain no courtyards or connector bodies, so pad avoidance cannot establish mating connector or wire clearance.

Source SHA256:`7e6f727a33c201fb72aaaaa1594ccaabde2608f28698f632ac196adcf04269a4`. KiCad 9 Python loaded the source and moved all 24 electronics **in memory only** to validate the candidate rotations and pad centers. The saved source hash stayed unchanged. Native courtyard boundaries agree with the study transform within 3.2e-14 mm. Geometry calculations use KiCad's pad and courtyard polygons and the actual curved outline, rather than just its bounding box. The saved source has **two copper layers**; a four-layer study is proposed by root and is a prerequisite for the inner-layer reservation described here. No physical stack thickness or copper weight is selected by this study.

## Candidate arrangement and physical pin maps

Q1/Q2 form a vertical pair on the right; Q3/Q4 form a vertical pair on the left. All four are180degrees. The native footprint origin and gate pin differ between packages:

- LFPAK88 Q1/Q2: pad1=gate, pads2/3/4=source on VIN_RAW, repeated mounting-base pad5=drain on MID. After180degrees the source fingers and gate face right, drain copper faces left; **gate is the bottom right finger**. Gate centers are Q1 (133.820,87.350) and Q2 (133.820,96.800). Source centers at X133.820 are Q1Y85.350/83.350/81.350 and Q2Y94.800/92.800/90.800. Main drain centers are(129.350,84.350)/(129.350,93.800). Pin mapping verified against [Nexperia PSMN1R3-80SSF](https://assets.nexperia.com/documents/data-sheet/PSMN1R3-80SSF.pdf).
- LFPAK56E Q3/Q4: pads1/2/3=source on MID, pad4=gate, pad5=drain on VOUT. After180degrees source fingers and gate face right, drain copper faces left; **gate is the top right finger**. Gate centers are Q3 (122.970,82.890) and Q4 (122.970,93.590). Source centers at X122.970 are Q3Y86.710/85.440/84.160 and Q4Y97.410/96.140/94.860. Drain centers are(119.700,84.800)/(119.700,95.500). Pin mapping verified against [Nexperia PSMN2R0-55YLH](https://assets.nexperia.com/documents/data-sheet/PSMN2R0-55YLH.pdf).

TP9 supplies the right-facing VIN source fingers. MID runs from the upstream left-facing drains to the downstream right-facing source fingers. VOUT drains transfer to a broad inner copper corridor and reach J3 without using the tiny J1/J3 hole-row gap. GND from TP8 can remain on the left toward J2. A layer assignment and actual via anti-pads must be established before routing; four layers do not automatically make every region available to all four nets.

U1 is between the downstream devices with C3 and R14 adjacent. U2 is in the right wing with C1 above and C2 below; this gives C2 more separation from the power package than the initial packing trial. [TI's layout guidance](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf) calls for short source/gate connections and keeping the charge-pump capacitor away from MOSFET heat. [onsemi's layout guidance](https://www.onsemi.com/pdf/datasheet/ncv68261-d.pdf) calls for nearby transistors/capacitors and power planes. C2 thermal exposure still needs examination on the actual copper layout. Optional D2/D3/C5 and R8 are below the connector row; their longer paths are explicit limitations, particularly if C5 is fitted for EMC improvement.

| Reference | Xmm | Ymm | KiCaddegrees |
|---|---:|---:|---:|
| Q1 | 130.0000 | 84.3500 | 180 |
| Q2 | 130.0000 | 93.8000 | 180 |
| Q3 | 120.3000 | 84.8000 | 180 |
| Q4 | 120.3000 | 95.5000 | 180 |
| U1 | 119.9000 | 89.4000 | 0 |
| U2 | 140.1000 | 93.8000 | 0 |
| C1 | 140.5000 | 91.1000 | 180 |
| C2 | 140.1000 | 97.0000 | 0 |
| C3 | 122.5000 | 89.4000 | 270 |
| C4 | 114.5000 | 97.8000 | 0 |
| C5 | 132.5000 | 103.5000 | 0 |
| D1 | 112.8000 | 94.5000 | 0 |
| D2 | 137.0000 | 104.9000 | 0 |
| D3 | 120.5000 | 106.2000 | 0 |
| R1 | 135.7000 | 87.0500 | 90 |
| R2 | 138.4500 | 86.8000 | 90 |
| R3 | 136.7000 | 97.8000 | 90 |
| R4 | 143.2500 | 95.0000 | 90 |
| R5 | 124.6250 | 82.1500 | 90 |
| R6 | 121.0000 | 80.6000 | 0 |
| R7 | 122.3000 | 91.7000 | 0 |
| R8 | 116.8000 | 108.8000 | 0 |
| R13 | 128.0000 | 103.5000 | 0 |
| R14 | 124.3000 | 89.4000 | 90 |

All these components remain on F.Cu. No rear-mounted components are assumed.

## Geometric checks and local connections

Courtyard checks use at least 0.5mm to the actual board polygon,0.25mm from the courtyard to fixed pad copper, and0.1mm additional courtyard-to-courtyard gap. Every component passes. The tightest values are:

- Edge: C1 courtyard to outline=0.542mm.
- Fixed pad: Q1 courtyard to TP7pad1=0.252mm.
- Additional courtyard gap: C3–R7=0.100mm. The original courtyards already include their footprint body/pad allowances; this is an extra assembly separation.

Straight pad distances below quantify local component proximity; they are **not route lengths** and do not prove an obstacle-free connection.

| Connection | Centerdistance,mm | Copperedgedistance,mm |
|---|---:|---:|
| R1.2 → Q1.1 | 2.191 | 0.861 |
| R3.2 → Q2.1 | 2.885 | 1.705 |
| R5.2 → Q3.4 | 2.278 | 1.169 |
| R7.2 → Q4.4 | 1.896 | 1.065 |
| C1.1 → U2.5 | 3.677 | 2.975 |
| C1.2 → U2.2 | 2.549 | 1.699 |
| C2.1 → U2.4 | 2.252 | 1.275 |
| C2.2 → U2.5 | 2.252 | 1.275 |
| C3.1 → U1.6 | 1.695 | 0.975 |
| C3.2 → U1.5 | 1.859 | 1.051 |
| R14.2 → U1.1 | 5.313 | 4.595 |
| R14.1 → Q4.3 | 4.822 | 3.940 |

Each individual gate resistor can connect to its MOSFET gate in approximately2–3mm straight distance. Gate driver branch routes still need a deliberate plan: the Q1 branch from U2 must detour around TP9's plated pad/hole. Match the two branches within each parallel bank where practical, keep source references separate from load-current copper, and check gate-loop inductance and transient sharing. A short via or a suitably chosen control layer may be required. R14's S_KELVIN side is adjacent to U1; sense pickup must be from the MOSFET source copper locally, not from the load-current neck.

## Prospective copper room and concrete bottlenecks

These are spatial reservations, not routed pours or current-capacity results. The assumption here is0.25mm separation from unrelated pad copper. Selected fab and electrical requirements may require more.

- **VOUT**: between the bottom edges of TP8/TP9 pads atY91.290094 and the top of the connector row atY99.540031, the theoretical continuous horizontal height is**7.750mm** after0.25mm pad setbacks. A conservatively inset reservation atX118.0–143.1/Y91.6–99.2 is**7.6mm high**. On an inner layer, front SMT pads do not consume that whole region; through-via anti-pads and control routing can. This corridor can reach the four J3 VOUT pads directly and use a larger VOUT area below them. Its actual necks depend on the final vias.
- **MID**: each downstream source group exposes**3.250mm** of combined vertical span. The facing source-to-upstream main drain copper gap is**3.935mm** in X; the courtyard gap alone is1.675mm. The two MID bridges can expand vertically around source lands and join upstream drain spreading copper; each branch ultimately tapers to three source lands. R7 is placed above Q4 rather than in this bridge. Expect about3.25mm minimum unobstructed finger-bank span per branch before final details, at nominal30A/device only if sharing is equal. This is a bottleneck requiring a current/thermal calculation.
- **VIN**: the three source lands on each LFPAK88 have5.200mm combined vertical span. The input rail must taper against the upper outline. At the top of Q1's source copper, the projected room from the source right edge to an outline setback of0.5mm is only**3.213mm**; this is not a uniform8mm input bus. Current into individual fingers, layer participation and placement of source stitching must be modeled.
- **Connector row**: J1pad7 and J3pad1 are2.5mm center-to-center with 1.5mm pads. Only**1.0mm** raw copper-edge space, or**0.5mm** after two 0.25mm clearances, remains between them. Crossing the full MID/current bank through this gap is a concrete spatial conflict. Both banks are kept above the row to avoid that failure.

The illustration `prospective-corridors.svg` marks useful space across layers. It does not assert that the full rectangles can be copper after every future via and signal is included.

## Hypothetical via array space

For geometry only, OD0.6mm/drill0.3mm vias at 1.0mm pitch have room for a3×6 grid (2.6×5.6mm envelope) inside each LFPAK88's3.74×6.8mm main drain land, and a3×4 grid (2.6×3.6mm) inside each LFPAK56E's3.3×4.2mm land. A3×2 grid (2.6×1.6mm) can fit a wider part of each MID branch. These counts are **not via-current recommendations**. Vias in solder lands require a approved filled/capped process or redesign outside the lands, with solder-wicking and voiding checks. Arrays on MID, VIN and VOUT create anti-pads on other net planes and must be included in neck measurements. Via plating, board thickness, temperatures and sharing remain unknown.

## Footprint/fabrication observations

The initial board's global minimum copper clearance, mask expansion and mask minimum web are all 0 mm; copper-to-edge setting is0.5mm. This is not a qualified rule set. All added SMT pad mask expansions are0; original fixed pads use+0.030mm mask expansion.

Intrinsic different-net copper gaps from the initial footprint pad polygons are LM74500 U2**0.200mm**, NCV U1side-to-exposed pad**0.220mm** and side-neighbor**0.300mm**, LFPAK88gate/source**0.800mm**, LFPAK56Egate/source**0.570mm**. A global0.25mm clearance rule would flag the controller footprints even before routing, so manufacturer-specific fine-pitch exceptions must be agreed with the fab and encoded deliberately.

**Pending NCV correction:** root has visually checked official onsemi511DW and reports the rotated recommended exposed land is0.95×1.65mm, compared with 0.90×1.60mm in this snapshot. The corrected side-to-EP gap becomes**0.195mm** and courtyard is unchanged. This study has not edited the footprint. The root's correction requires a new source hash and native validation. That0.195mm gap matters for heavy copper and soldermask process acceptance.

All fixed PTH annular rings are approximately0.250mm (minimum0.249988mm from slight pad-width rounding). As one current primary manufacturer example, [JLCPCB's published capabilities](https://jlcpcb.com/capabilities/pcb-capabilities/) give2oz multilayer minimum track/space0.15/0.15mm,2oz mask pad spacing0.20mm, and2oz PTH annular rings at least 0.254mm. Thus the unchanged fixed rings fall about4µm short of that stated rule, and corrected NCV EP gap0.195mm is below its cited2oz mask threshold. Obtain chosen-fab acceptance or change the permitted copper/mask geometry; neither can be assumed from a generic2oz copper request. This example does not select a manufacturer or qualify the board.

Saved masks at0 expansion would geometrically leave0.200mm between U2neighbor openings and0.220mm to U1's initial EP. Expanding each by0.050mm would reduce these to0.100/0.120mm; after the proposed EP correction the latter is0.095mm. Actual fabrication registration, mask color/process and land dimensions must be checked.

## Decision and remaining work

The fixed polygon does not force a four-package spatial impossibility. This all-top candidate is suitable for a clearly labeled placement study and native routing preparation, **conditional** on actual connector body clearances, verified controller lands, a fabricator-approved heavy-copper rule set, and an explicit multilayer power/return and via plan. No cooling area,60 A thermal result, connector rating, complete power route or fabrication approval has been demonstrated. Native filled-zone DRC, source/gate-loop review, via/plane neck analysis, coupled electrothermal modeling and hardware qualification remain required.

Companion files: `candidate-positions.json`, `placement-metrics.json`, `native-memory-validation.json`, `candidate-all-top.svg/png`, `prospective-corridors.svg/png` and `geometry.json`. Only work/ files were written.
