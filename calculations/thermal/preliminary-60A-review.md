# Preliminary 25 V / 60 A review of the existing four-MOSFET draft

Date: 15 October 2026. Status: **engineering screening only; not production qualified**.

The existing 2+2 design has **6.48 W** of calculated MOSFET conduction loss at its quoted 25°C resistance points and **12.78 W** in the mixed hot resistance case, **conditional on establishing at least 10 V drive at each front MOSFET gate**. The downstream devices dissipate **4.41 W each** in the hot case. Retention of these four parts for 60 A continuous service requires a demonstrated cooling solution, rated terminations and completed fault protection. No PCB was edited for this review. These calculations are independent analytical estimates, not Saturn output or physical validation.

## Inputs and scope

- Q1/Q2: PSMN1R3-80SSFJ, two parallel upstream devices; Q3/Q4: PSMN2R0-55YLHX, two parallel downstream devices. MPNs were checked against the project BOM.
- 25 V / 60 A is the new request. For screening, 60 A is treated as continuous. Actual continuous/peak duty, duration, ambient, airflow, enclosure and cooling remain unknown. The earlier 6S full-charge envelope was 25.2 V; it still needs reconciliation with the new 25 V limit.
- Each device carries 30 A only under equal sharing. Real sharing depends on resistance, thermal coupling and layout. Device resistance is quoted at 25 A test current; applying it at 30 A is an engineering screening model, not a new guaranteed manufacturer specification.
- Front resistance assumes at least 10 V gate drive; this has not been verified at the actual gates. LM74500 Table 6.5 specifies VCAP-to-SOURCE thresholds, not an explicit guaranteed fully charged GATE-to-SOURCE minimum. Its VCAP minimum is 8 V at SOURCE=3.2 V and the stated light-load condition. Normal 6S operation is expected to provide adequate pump voltage, but a complete-system 10 V gate-drive guarantee does not follow from those thresholds alone. Downstream uses the conservative 4.5 V characterization, compatible with the NCV controller's 9 V charged-gate specification in its stated supply region. Actual loaded gate waveforms and minima must be established.
- Copper, vias, contacts, wires, solder and controller losses are excluded from the MOSFET table. Native-editor unsaved state was not inspected.

Snapshot file SHA256: `7e6f727a33c201fb72aaaaa1594ccaabde2608f28698f632ac196adcf04269a4`. Geometry is from the saved file as read; routing or unsaved edits made later may differ.

## MOSFET conduction calculation

For two parallel identical devices per bank: Rbank = Rdevice/2, Vdrop = I × Rtotal, Pbank = I² × Rbank, and Pdevice = (I/2)² × Rdevice. [Front manufacturer datasheet](https://assets.nexperia.com/documents/data-sheet/PSMN1R3-80SSF.pdf) specifies 1.2 mΩ at 25°C, 2.2 mΩ at 105°C and 2.8 mΩ at 175°C, each at 10 V drive. [Downstream manufacturer datasheet](https://assets.nexperia.com/documents/data-sheet/PSMN2R0-55YLH.pdf) specifies 2.4 mΩ at 25°C and 4.9 mΩ at 150°C at 4.5 V drive.

| Quoted resistance case | Total R, mΩ | Drop at 60 A, mV | Front bank / each, W | Downstream bank / each, W | MOSFET total, W |
|---|---:|---:|---:|---:|---:|
| 25C quoted resistance | 1.800 | 108.0 | 2.160 / 1.080 | 4.320 / 2.160 | 6.480 |
| mixed hot quoted resistance | 3.550 | 213.0 | 3.960 / 1.980 | 8.820 / 4.410 | 12.780 |
| higher-temperature quoted resistance | 3.850 | 231.0 | 5.040 / 2.520 | 8.820 / 4.410 | 13.860 |

The hot cases mix specified junction temperatures. They are not a self-consistent thermal operating point or guaranteed circuit-level loss bound. Front resistance and all totals additionally depend on proof of at least 10 V gate drive; the quoted resistance cannot be applied as a guaranteed maximum at an unverified lower gate voltage. In particular, 2.2 mΩ at 105°C is not a universal hot maximum. A final electrothermal model must iterate R(T), current sharing and the actual thermal paths. At 25 V / 60 A the input power is 1500 W: a sub-1% electrical loss can still leave over 12 W concentrated in this small board. [TI gate/pump specifications](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf)

At 60/45 times the previous current, equal-resistance conduction heating rises by (60/45)² = **1.778**. The former six-device 2+4 allocation would have 4.32 W cold / 8.37 W in the same mixed hot case; reverting to six does not qualify its connectors, cooling or balance paths either. In the four-device hot case, a 60/40 current split instead of 50/50 gives downstream currents 36/24 A and losses 6.35/2.82 W: the hotter member is substantially above the equal-sharing estimate.

## Thermal screen and production implication

Illustration only: assume ambient 60°C and target junction 125°C, allowing 65°C rise. With the mixed hot resistance case, isolated effective junction-to-ambient resistance must be no greater than **32.8°C/W per front device** and **14.7°C/W per downstream device**. Using the higher-temperature front resistance tightens its budget to **25.8°C/W**. Even at assumed ambient 25°C, the downstream hot-case budget is 22.7°C/W.

The cited front datasheet gives typical 35/70°C/W reference-board examples, and the downstream datasheet gives 42/85°C/W; the lower values use a 25.4 mm-square, 70 µm copper region. These are reference layouts, not guaranteed resistances on the company board. The preserved outline bounding box is approximately 44.57 × 41.56 mm in the existing comparison report, so four independent 25.4 mm-square heat-spreading regions cannot simply be assumed. Four layers are thermally coupled; they do not produce four independent cooling surfaces.

Use Tj,i = Ta + sum(θij × Pj) for a coupled thermal model. The optimistic shared-board budget 65/12.78 = **5.09°C/W** already uses the entire temperature rise before junction-to-board differences and other losses. It is a necessary screening ceiling, not an achieved board thermal resistance.

Do not release the present four devices for 60 A continuous based only on package current ratings or a wide Saturn trace result. They can be retained only if a verified thermal path meets the actual ambient/duty and temperature targets. Otherwise lower resistance devices, a larger/direct-cooled package, heatsink/cold plate, more copper or increased device count is necessary. As a selection screen, a 1 W-per-device budget at 30 A requires RDS(on) ≤1.11 mΩ at the worst intended junction temperature and available gate drive. A quoted 25°C resistance alone is inadequate.

A shared heatsink must not electrically short MID and VOUT drain copper. Insulating thermal interfaces, mechanical mounting and their resistance require design review. MOSFET heat must also keep both controllers within their temperature ratings. [onsemi](https://www.onsemi.com/pdf/datasheet/ncv68261-d.pdf) provides no controller thermal shutdown to protect the power transistors.

## Fixed holes, contacts and terminations

The saved pad geometry has J2/J3 at 2.50 mm pitch, each with four nominal 1.5 mm pads and 1.0 mm holes; TP8/TP9 each have one nominal 2.5 mm pad and 2.0 mm hole. Pad annular width is approximately 0.25 mm. Connector and cable MPNs and allowable all-contact-loaded current are unknown. A hole diameter is not a connector current rating.

At 60 A, each of four perfectly shared contacts needs **15 A**. If one opens, the remaining three need 20 A each. Each input termination needs the full 60 A. A 2 mm hole has a theoretical solid-circle area of 3.142 mm² before insertion clearance; this does not establish the fitted wire area, crimp/solder quality or allowable ampacity. Fixed dimensions may prevent use of a suitable rated termination. Preserve the mechanical evidence, but resolve that conflict before production; routing cannot remedy an underrated connector.

Hypothetical contact-resistance sensitivity, not specifications of the existing connector:

| Assumed resistance per contact, mΩ | Each 15 A contact loss, W | One four-contact rail, W | Both output rails, W |
|---|---:|---:|---:|
| 1 | 0.225 | 0.900 | 1.800 |
| 3 | 0.675 | 2.700 | 5.400 |
| 5 | 1.125 | 4.500 | 9.000 |
| 10 | 2.250 | 9.000 | 18.000 |

Every additional 1 mΩ in the complete 60 A path contributes another 3.6 W and 60 mV. Datasheet resistance/derating, current sharing, contact cycling and assembly tests are required for the actual terminations.

For perspective only, the following barrel-only R = ρL/A model assumes a 1.6 mm board, 25 µm plating and representative annealed copper resistivity 1.7241×10⁻⁸ Ω·m at 20°C. A = π[(D+2t)²−D²]/4. Fabrication thickness, plating and current distribution are currently unknown. These are **not Saturn or IPC current-capacity results**; lead/solder paths and spreading resistances are excluded.

| Finished hole assumption, mm | Assumed barrel current, A | Barrel copper area, mm² | Barrel R at 20°C, mΩ | Barrel-only loss, W |
|---|---:|---:|---:|---:|
| 1 | 15 | 0.08050 | 0.3427 | 0.0771 |
| 2 | 60 | 0.15904 | 0.1734 | 0.6244 |

Temperature increases copper resistance. Add appropriately designed low-resistance stitching where current transfers layers; do not force the full transfer through one barrel or narrow thermal-relief spokes. Exact via sizing/count depends on the fabricated stackup and a verified current split. [TI board-layout guidance](https://www.ti.com/lit/pdf/slva959) and [CDA conductivity reference](https://copper.org/applications/industrial/DesignGuide/props/electrical.php) provide the relevant background; they do not validate these unidentified connectors.

## Startup, reversal and balance interface

Both power banks are forward body-diode conductive before their gates are enhanced. The [TI controller datasheet](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf) requires startup/body-diode current assessment and external overload/short-circuit protection. This draft does not regulate output inrush, isolate positive overvoltage or limit short-circuit current. Front 1 µF charge-pump capacitance gives approximately 21.7 ms typical enable delay under its cited test-point equation; the load can already receive power through the body diodes. Actual 60 A startup, load capacitance and harness inductance require pulse/SOA measurements or an adequate model. The 3 A MID clamp D1 is not proven capable of arbitrary hot-reversal fault energy.

Balance protection remains **unimplemented**: saved schematic netlist endpoints J1 and TP1–TP7 are intentionally open. A new DXF defines geometry, not receiver pin tolerances, current limits or safe misconnection behavior. Directly reconnecting raw G/B1–B6 can bypass the main switch. For example, swapping the main leads while raw balance G remains tied to receiving-electronics ground can create a battery-short path through that balance conductor and the reversed main return. B6 or intermediate taps can also back-power downstream electronics. Neither four nor six main MOSFETs prevents those faults.

Production gates are therefore: define continuous/peak duty and ambient/cooling; specify fabricated copper and plating; qualify or replace terminations; complete balance protection for an identified receiver; assess startup/reversal/short-circuit energy and upstream fuse/BMS response; then perform coupled thermal/current-sharing analysis and hardware tests. ERC/DRC and Saturn calculations cover particular CAD/current estimates, not all of these electrical and thermal conditions.

Companion machine-readable evidence: `preliminary-60A-review.json`. No physical test, temperature measurement or completed 60 A qualification is claimed.
