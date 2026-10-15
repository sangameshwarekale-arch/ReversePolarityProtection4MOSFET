# Two-sided 24 V / 25.2 V maximum / 45 A placement review

**Preferred conditional placement found.** All 36 existing footprints and electrical pad nets are preserved. Four power MOSFETs remain on the front; 18 controller/support components move to the rear. Two proposed M5 power output terminals use the lower lobes. The minimum added same-side courtyard gap rises from **0.100 to 0.500 mm**. No tracks, vias or zones were created. Routing starts only after the user approves this placement.

This is a concrete placement proposal, not a 45 A thermal, mechanical or manufacturing release. The source is the working project snapshot with four copper layers, zero tracks/vias/zones, 60 outline primitives and 12 fixed mechanical footprints. The saved native geometry matches the Desktop working board per root inspection. Source SHA256: `291e8b6199c2fc2242c567669cc0f1837f2036e35f740affb53d9157cf03d2e6`. Only files in this work directory were written by the placement study.

## Arrangement and what changed

- Q1/Q2 stay as a right-side upstream bank; Q3/Q4 stay as a left-side downstream bank. All are at native 180 degrees, with source/gate fingers facing right and drains facing left. Q1/Q2 gate is the bottom finger; Q3/Q4 gate is the top finger. Slight Y adjustments increase clearance to fixed pads and between the upstream packages.
- Front low-current congestion is removed. U1, U2, R1–R8, R14, C1–C5 and optional D2/D3 move rearward. D1 stays on the front near the left power region; R13 moves to the lower middle between the proposed output terminals. No part values or intended connections change.
- U1 and C3 occupy the gap between downstream packages, not the backside of a drain pad. U2 is to the right of the upstream drain copper. The closest controller-courtyard projection to any front MOSFET drain copper is **0.425 mm for U1** and **3.805 mm for U2**. This avoids direct drain-pad stacking but does not prove controller temperature: planes, the board and both power banks remain thermally coupled.
- J4 VOUT and J5 GND are proposed full-current output locations. Existing J2/J3 are retained on their original nets with their ratings still unknown. Adding rated candidate posts does not qualify the raw input TP8/TP9 terminations or the old headers.

Rear references: **C1, R6, U1, R8, R14, R4, R3, C3, C4, D3, D2, R2, C5, C2, U2, R7, R1, R5**. There are 18 rear parts, 6 existing front electronics, 12 fixed front mechanical footprints and 2 new front posts: 38 physical parts in the proposed complete placement.

## Native coordinates and mirroring

Angles in `candidate-positions.json` are **final native KiCad orientations** after flipping to the requested side. Apply `f.Flip(f.GetPosition(), pcbnew.FLIP_DIRECTION_LEFT_RIGHT)` only if the side differs, then set the stored orientation and position. Do not mirror X manually or reuse a front-side pad map. All reported coordinates remain absolute top-view board coordinates. The rear comparison panel is horizontally mirrored for viewing from below; its labels are intentionally readable.

| Ref | Side | X mm | Y mm | Final KiCad degrees |
|---|---|---:|---:|---:|
| Q1 | front | 130.000 | 84.700 | 180 |
| Q2 | front | 130.000 | 94.300 | 180 |
| Q3 | front | 120.300 | 85.300 | 180 |
| Q4 | front | 120.300 | 95.500 | 180 |
| D1 | front | 112.800 | 94.500 | 0 |
| R13 | front | 127.000 | 105.000 | 0 |
| U1 | back | 123.800 | 89.700 | 180 |
| C3 | back | 120.600 | 89.375 | 270 |
| C4 | back | 119.900 | 93.000 | 180 |
| R5 | back | 124.500 | 83.390 | 180 |
| R6 | back | 124.500 | 85.600 | 180 |
| R7 | back | 124.500 | 93.800 | 180 |
| R8 | back | 124.500 | 96.000 | 180 |
| R14 | back | 128.000 | 87.250 | 180 |
| D3 | back | 128.100 | 89.700 | 180 |
| C5 | back | 128.000 | 92.400 | 180 |
| U2 | back | 137.100 | 93.500 | 180 |
| C1 | back | 140.400 | 93.500 | 90 |
| C2 | back | 137.100 | 97.000 | 180 |
| R1 | back | 132.700 | 87.700 | 0 |
| R2 | back | 132.700 | 85.500 | 0 |
| R3 | back | 132.700 | 97.300 | 0 |
| R4 | back | 132.700 | 95.100 | 0 |
| D2 | back | 132.600 | 91.400 | 90 |

## Clearance and circuit-preservation checks

Native KiCad was used in memory to flip and place every moved component. The source file was not saved. Reference sets, values, library footprint IDs and every numbered pad's net, size and drill remain identical. All 12 fixed footprint snapshots are exactly unchanged. New terminals are separate proposed circle/pad geometry; the native project now implements these footprints and schematic symbols, with fresh saved-file checks under ../reports/.

All existing component courtyards are polygon-contained; the actual curved outline was used. Same-side courtyards are checked independently for front and rear. All original through-hole pads are obstacles on **both** sides. Ordinary opposite-side SMD pads may overlap in XY because they occupy different copper surfaces; that is not a connection or a clearance violation by itself.

| Check | Proposed minimum |
|---|---:|
| Additional same-side courtyard separation | 0.500 mm, C1/U2 |
| Upstream power-package courtyard gap | 0.510 mm |
| Existing electronics courtyard to any fixed through-pad copper | 0.515 mm, U2/TP9 |
| Existing electronics courtyard to outline | 0.994 mm, D1 |
| New terminal engineering courtyard to outline | 0.524 mm, J5 |

The fixed footprints contain only pad/graphic evidence, with no verified connector body, mating, insertion, screw or wire envelopes. None of these clearance numbers proves that a tall existing header housing or wire harness clears a lug or driver.

## Gate, sense and decoupling paths

The following are pad-centre XY offsets, **not routed lengths**. Opposite-side overlapping pad projections still require a deliberate via and traces.

| Connection | XY offset mm |
|---|---:|
| R1.2 → Q1.1 | 0.295 |
| R3.2 → Q2.1 | 0.295 |
| R5.2 → Q3.4 | 0.705 |
| R7.2 → Q4.4 | 0.736 |
| C1.1 → U2.5 | 4.604 |
| C1.2 → U2.2 | 2.050 |
| C2.1 → U2.4 | 2.549 |
| C2.2 → U2.5 | 2.549 |
| C3.1 → U1.6 | 2.334 |
| C3.2 → U1.5 | 2.334 |
| R14.2 → U1.1 | 3.052 |

R1/R3 backside MOSFET-side pads are only 0.295 mm from the gate-pad centres in XY; R5/R7 are 0.705/0.736 mm away. Use nearby ordinary tented signal vias outside the solder lands, not an unapproved drilled via inside a gate/resistor solder pad. One possible set of via locations is below. These are 0.6 mm OD / 0.3 mm drill geometry hints only; actual drill/plating and routes require fabrication rules and approval.

| Hint | XY mm | Net | Minimum unrelated pad-copper gap mm |
|---|---|---|---:|
| gate Q1 | [134.9, 87.7] | Net-(Q1-G) | 1.235 |
| gate Q2 | [134.9, 97.3] | Net-(Q2-G) | 0.450 |
| gate Q3 | [124.1, 82.5] | Net-(Q3-G) | 0.698 |
| gate Q4 | [124.1, 92.7] | Net-(Q4-G) | 0.817 |
| MID Kelvin pickup candidate | [124.9, 86.7] | /MID | 0.817 |
| controller VIN pickup | [134.9, 90.4] | /VIN_RAW | 1.660 |
| U2/C1 GND return | [139.6, 91.0] | /GND | 0.799 |
| C1 VIN connection | [142.0, 91.0] | /VIN_RAW | 1.493 |
| C3 GND return | [119.6, 90.2] | /GND | 1.043 |
| U1 GND return | [121.8, 89.7] | /GND | 0.700 |

The four gate-via hints leave no pad overlap on either side. They support short roughly 2.4–2.7 mm combined front/rear lateral gate connections before allowing for board thickness and trace shaping. The controller-to-resistor branches still need matching: the shorter parallel-bank branch has roughly 2 mm less straight-line distance in each bank, which can be accommodated when routing. Do not match only total conductor length while ignoring shared-source inductance. Route a separate source reference with the gate return; R14's sense connection is 3.052 mm straight from U1's S input, and its MID pickup must be Kelvin connected locally, separate from the main load-current neck.

C2 has two symmetric 2.549 mm straight connections to U2 VCAP/SOURCE. Keep those on the rear and avoid placing a VIN trace across the VCAP branch. C3 has symmetric 2.334 mm links to U1 IN/GND. C1 is rear-right of U2: its 2.050 mm GND and 4.604 mm SOURCE offsets require a local GND return and a separate VIN feed; using the proposed VIN/GND via hints above the output corridor avoids a rear trace crossing the charge-pump capacitor route. Capacitor effective value, placement temperature, EMC and turn-off waveforms remain qualification items. D2/D3/C5 remain DNP; if fitted, their loops must be reviewed rather than assuming their nominal values guarantee EMC or clamping.

## Prospective routing channels

These are space reservations to guide routing after approval, not copper-zone definitions or ampacity results.

- VIN_RAW: TP9 feeds right-facing Q1/Q2 sources. The source fingers span 5.2 mm vertically per device. The upper rail must taper with the curved outline; it is not an 8 mm uniform bus. Control pickup can use a separate via above the output corridor.
- MID: Q1/Q2 left drain lands face the right source fingers of Q3/Q4. The facing main-drain/source copper edges are approximately 3.935 mm apart in X. Each downstream source group spans 3.250 mm in Y; the front has no small resistors occupying these bridges now. Each branch still tapers to three source fingers and needs current-sharing, resistance and temperature checks.
- VOUT: a broad inner-layer corridor remains available at X118.0–143.1, Y91.6–99.2: **7.6 mm** reserved height. The theoretical pad-limited height between the TP8/TP9 bottom edges and connector-row top edges is 7.750 mm with assumed 0.25 mm unrelated-pad setbacks. Front and rear SMD bodies do not by themselves prevent inner copper. Signal via anti-pads and all future power-transfer arrays do affect it. With 0.6 mm through vias and 0.25 mm net clearance, a different-net via removes a 1.1 mm circular area from this layer. The Q2/Q4 gate-via hints would each reduce one local projected 7.6 mm cross-section to 6.5 mm total copper, with the larger uninterrupted sub-band about 5.15/5.95 mm respectively. Local widening may help, but the final filled polygons must be measured after every array/anti-pad is present.
- The full-current VOUT path can cross the legacy row through the **same-net J3 region** into the J4 lower lobe; it must not pass through the raw J1/J3 gap. The J1pad7/J3pad1 raw gap is only 1.0 mm, or 0.5 mm after two 0.25 mm clearances. Existing J3 holes remove copper even though their pads share VOUT, so count the hole cross-sections when calculating the final effective neck. Do not count an unrated old header as the power conductor.
- GND: TP8 can reach J5 through the left-side return region, with the same-net J2 row retained. D1's MID pad must be isolated from GND; rear/inner participation is available, but full-current layer transfers and terminal vias need calculation. The new SMT posts have no drill, so any required layer transfer must be intentionally designed.

No power-via count is selected. Via-in-pad under large MOSFET/terminal solder lands requires an approved filled/capped process or a layout outside the lands; ordinary open holes can drain solder. Final anti-pads, minimum necks, current split, copper weights and stack thickness remain unresolved. Use root's independent 45 A review for electrical/thermal screening; no Saturn results are fabricated here.

## New terminal and mechanical reservations

Candidate: **Würth 7466205R** M5 blind-thread SMT terminal, listed 70 A, nominal body Ø9 × 7 mm, single solid Ø10 mm land, no pin/drill; engineering courtyard Ø11 mm. These are nominal dimensions subject to the drawing's general tolerances. Published current depends on board, lug and wire. The actual 45 A assembly is not established by the catalogue rating. [Official terminal datasheet](https://www.we-online.com/components/products/datasheet/7466205R.pdf).

| Ref | Centre XY mm | Courtyard/outline gap mm | Courtyard/fixed-pad gap mm | Assumed Ø12 tool/fixed-pad gap mm |
|---|---|---:|---:|---:|
| J4 | [137.975, 107.525] | 0.525 | 1.004 | 0.504 |
| J5 | [115.475, 107.525] | 0.524 | 1.004 | 0.504 |

The preferred cable-lug candidate is Würth 5580506 M5/6 mm² (10 mm width, 21 mm total length); 5580510 M5/10 mm² (12 × 22 mm) is an alternative. Wire ampacity and bend radius still depend on installation. The magenta drawing shows a **conservative engineering** 12 mm wide, screw-axis Y−6 to Y+22 reservation toward the lower edge. It is not a reconstruction of the lug's hole-centre geometry, and total lug length must not be interpreted as cable-exit distance from the screw axis. The intended cable exit is toward +Y/outside the board. [5580506](https://www.we-online.com/components/products/datasheet/5580506.pdf), [5580510](https://www.we-online.com/components/products/datasheet/5580510.pdf).

The tool result assumes a 12 mm diameter circular driver/socket projection around the screw axis; only existing pad copper has been tested. Connector bodies, lug thickness, washer/head diameter, tool approach and vertical access are not known. The 7 mm body height excludes lug, hardware and driver. Screw length/thread engagement and torque-controlled assembly remain mechanical selections. The nominal 2.2 N·m terminal tightening limit is not a demonstrated PCB bending or cable pull rating. Provide cable strain relief and an insulating underside support/clamp design.

Radius-6 mm underside support projections around J4/J5 have no rear components: minimum additional projection gaps are **3.550 mm** and **7.177 mm**. Thus rear parts do not consume those support regions; no support hardware has been designed or installed. The final saved native proposal places GND at (123.0,108.0) and VOUT at (130.2,108.0) mm on the posts' inner flanks, using 1.0 mm silkscreen text. The original Y101.8 suggestion conflicted with locked header graphics. Seven preserved silk labels were repositioned/resized; native DRC reports zero silkscreen warnings. Comparison net labels are diagram annotations; see the native front image for final production-label locations. Unknown header bodies still require mechanical checks.

## Rear height and assembly

Rear height screening uses root's retained manufacturer evidence: U1 max 0.8 mm, U2 max 1.1 mm, C1/C3 max 0.9 mm and C2/C4 max 1.4 mm. Official Yageo RC0603FR-0710RL and RC0603FR-071ML specify thickness 0.45±0.10 mm, hence 0.55 mm maximum for the fitted rear resistors. [10 Ω part](https://yageogroup.com/component-documentation/download/specsheet/RC0603FR-0710RL), [1 MΩ part](https://yageogroup.com/component-documentation/download/specsheet/RC0603FR-071ML).

The fitted-part maximum is 1.4 mm before assembled solder and board/enclosure variation. Adding an **assumed** 0.15 mm solder allowance and 0.50 mm free clearance gives a 2.05 mm minimum local rear cavity. A **3 mm nominal stand-off** is a practical starting mechanical reservation, not enclosure approval. Existing through-hole lead/solder protrusion, board warp, support contact, insulation requirements and cable/connector tails can require more. DNP components need actual height checks before fitting. Two-sided assembly cost, reflow order and support for the heavy front posts/FETs need assembler agreement.

## Release boundary

Approve or revise the concrete two-sided placement before routing. Remaining holds include: actual connector/lug/tool/strain-relief models and support; input termination rating; fabricated copper/stack/plating and rules; terminal stencil; 0.195 mm corrected NCV exposed-pad gap; power via arrays and final anti-pads; thermal environment and cooling; balanced power/gate/Kelvin routing; native filled-zone DRC/ERC/connectivity; and physical validation. Existing balance-interface protection remains as the preserved schematic defines it; placement does not add missing balance protection.

The native terminal footprint should currently carry **no F.Paste** until the manufacturer's 150 µm stencil and subdivided aperture drawing are independently reconstructed and checked. This is an explicit assembly/manufacturing hold. No manufacturing outputs or 45 A safety claim are justified by this placement study.

Files: `candidate-positions.json` (frozen native poses), `original-geometry.json`, `proposed-geometry.json`, `geometric-metrics.json`, `native-validation-and-routing-hints.json`, `placement-comparison.svg/png`, `proposed-front.png`, `proposed-rear-mirrored.png`. Native source was only read; all study edits are confined to work/redesign45/placement.
