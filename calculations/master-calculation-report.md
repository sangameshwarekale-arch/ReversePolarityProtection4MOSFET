# Master calculation report — 25 V / 60 A evaluation

15 October 2026. Project: [ReversePolarityProtection4MOSFET](../ReversePolarityProtection4MOSFET.kicad_pro).

**Authoritative status: preliminary four-layer placement, unrouted, not qualified for 60 A or fabrication.** The four MOSFETs are retained for engineering study only. No copper weight, physical stackup, via array, heatsink, rated power termination or balance-protection implementation is selected for production. This report consolidates the evidence below; it does not convert an analytical result or successful CAD check into hardware validation.

## Current native project and verification

The current [PCB](../ReversePolarityProtection4MOSFET.kicad_pcb) has 24 electronic footprints placed on F.Cu and 12 fixed mechanical footprints. Four copper layers are enabled, but this is a CAD layer setting rather than an approved manufactured stackup. There are **0 tracks, 0 vias and 0 zones**. All 60 outline primitives, fixed-footprint locations and fixed pad geometry are preserved exactly in the native comparison. Net assignments and schematic links are preserved. [Placement and preservation evidence](../reports/preliminary-60A-placement-validation.json).

The NCV exposed-pad copper was corrected to a **rectangular 0.95 × 1.65 mm** land. The proposed two 0.80 × 0.70 mm paste windows at y=±0.42 mm provide 71.45% rectangular-area coverage. Stencil, solder-mask and assembly acceptance remain pending. Its intrinsic side-pad-to-EP copper gap is **0.195 mm**, below the project's **0.200 mm screening minimum**; no DRC exclusions were used to hide this condition. Earlier roundrect-area percentages or smaller-EP geometry in exploratory documents do not describe the current rectangular pad. [Current dimensions and status](../reports/preliminary-60A-placement-validation.json), [manufacturing analysis](stackup/spacing-and-footprint-limits.md).

| Native check | Actual recorded result | What it establishes |
|---|---|---|
| ERC, current 60 A annotation | 0 violations | Symbol/net rule checking; balance endpoints are deliberately open |
| DRC, current placement | 66 unconnected items; 4 NCV clearance errors; 7 silkscreen warnings | Routing and clearance work remain; **DRC has not passed** |
| PCB/schematic parity within that DRC | 0 discrepancies | Compared schematic/PCB connectivity is consistent; this is not functional verification |

The seven silkscreen warnings comprise five silk-over-copper and two silk-overlap entries. See [current ERC](../reports/erc-preliminary-60A.json), [current DRC](../reports/drc-preliminary-60A-placement.json) and [schematic annotation update](../reports/schematic-60A-status-update.json). The 60 A title update left electrical nodes unchanged. Older starter DRC/ERC summaries are historical records, not the latest status.

Saturn PCB Toolkit **8.47** is running, but its calculator window is not exposed to the desktop-control interface. **No actual Saturn calculation result is available.** [Saturn access record](saturn-records/access-status.json). Separately, desktop-control launching of the KiCad manager was rejected with “not approved to use kicad”; reopening the project UI was not performed. Safe CLI checks supplied the native evidence above. User authorization for full PC access authorizes work, but does not provide the missing technical specifications or change these tool results.

## Calculation index and method boundaries

| File | Content and authoritative limitation |
|---|---|
| [Independent copper/via methods](independent-copper-via-methods.md) | Equations, assumptions, numerical examples and proposed layer roles; not final conductor sizing |
| [Independent method inputs](independent-method-inputs.json) | Copper constants and formula inputs; explicit unqualified/extrapolation status |
| [IPC-2221 comparison CSV](tracks/independent-IPC2221-comparison.csv) | Older coefficient/exponent model at stated currents and temperature rises; 60 A extrapolation, **not Saturn or IPC-2152** |
| [Rectangle resistance sensitivity CSV](copper/rectangle-resistance-sensitivity.csv) | Ideal same-net rectangular conductor resistance, voltage drop and Joule loss; no ampacity result |
| [Candidate corridor resistance CSV](copper/candidate-corridor-resistance.csv) | Placement-space geometry estimates for proposed VOUT/MID corridors; no actual routed zone or bridge |
| [Via barrel/array sensitivity CSV](vias/barrel-array-ohmic-sensitivity.csv) | Ideal barrel resistance under assumed thickness/plating and equal sharing; no safe-current-per-via rating or chosen count |
| [Fabrication capabilities](stackup/fabrication-capabilities.md) | Candidate vendor/process research; no chosen fabricator, contractual minimum copper/plating or approved physical stackup |
| [Spacing/footprint limits](stackup/spacing-and-footprint-limits.md) | Intrinsic gaps, ring/mask/stencil screens and manufacturing issues; read current rectangular NCV geometry above when earlier shape comments differ |
| [Preliminary 60 A thermal review](thermal/preliminary-60A-review.md) | Conditional MOSFET losses, thermal budgets, contact/barrel examples and release barriers |
| [Thermal calculation JSON](thermal/preliminary-60A-review.json) | Machine-readable cases, input assumptions, source records and unverified front gate-drive condition |
| [Controller and fault limits](thermal/controller-and-fault-limits.md) | Gate-drive/charge assumptions, body-diode startup, hot plugging/reversal and balance bypass scope |
| [Saturn access status](saturn-records/access-status.json) | Software/version/window availability; **contains no computed Saturn result** |
| [Earlier conduction comparison CSV](../reports/conduction-calculations.csv) and [JSON](../reports/conduction-calculations.json) | Historical **45 A** four-versus-six/allocation comparison; not the 60 A result set |

The geometry-preservation records are [original layout comparison](../reports/layout-starter-comparison.json), [DXF comparison](../reports/dxf-geometry-comparison.json) and the latest [native placement validation](../reports/preliminary-60A-placement-validation.json). The [exported netlist](../reports/netlist.xml) and [editable schematic](../ReversePolarityProtection4MOSFET.kicad_sch) define the current electrical draft.

The independent IPC-2221 calculation uses I=k×ΔT^0.44×A^0.725 with square-mil area and the stated external/internal coefficients. Its outputs must not be described as an installed Saturn run, IPC-2152 output, measured temperature rise or approved width. Ohmic resistance models use R=ρL/A; they answer resistance and electrical loss under their assumptions, not how the real board dissipates heat. Equal current division between layers or vias requires a connectivity/distribution model; enabling four layers does not automatically divide 60 A by four.

## Candidate copper-space result

For one proposed **25.1 × 7.6 mm** corridor, assume **70 µm finished copper and two identical same-net parallel paths**. The candidate CSV gives:

| Assumed copper temperature | Ideal R | Drop at 60 A | Loss at 60 A |
|---|---:|---:|---:|
| 20°C | 0.4067 mΩ | 24.4 mV | 1.464 W |
| 80°C | 0.5026 mΩ | 30.2 mV | 1.809 W |

These describe a spatial reservation and ideal rectangles only. There are no zones, transfer vias or validated parallel paths in the native board. Finite pad injection, necks, holes, bends, unequal layer routes and terminal losses are not represented. The values are not the full circuit-loop resistance and do not prove 60 A capacity or the assumed copper temperature. 70 µm is a modelling input, not a selected/guaranteed fabrication thickness. [Candidate cases](copper/candidate-corridor-resistance.csv).

## Four-device decision and unresolved electrical limits

The study retains two PSMN1R3-80SSFJ upstream and two PSMN2R0-55YLHX downstream. Each carries 30 A under ideal sharing. Quoted-resistance calculations give **6.48 W / 108 mV** at 25°C points and **12.78 W / 213 mV** using front resistance at 105°C and downstream resistance at 150°C. The latter is a mixed-temperature sizing case, not a thermal equilibrium. The higher-temperature quoted-point case gives 13.86 W. All totals exclude copper/contacts and remain conditional on adequate front gate drive: the front resistance specifications require 10 V, while the TI VCAP thresholds do not directly guarantee the actual loaded gate minimum. [Calculation conditions](thermal/preliminary-60A-review.md), [gate qualification](thermal/controller-and-fault-limits.md).

For an illustrative, **not user-confirmed**, 60°C ambient/125°C junction target, the downstream mixed-hot loss of 4.41 W per device requires isolated effective θJA≤14.7°C/W. The reference 42/85°C/W board examples do not substantiate this. Mutual heating, assembly, current imbalance and conductor/connector losses tighten the cooling problem. Retention for production would require a verified thermal path over the actual duty and environment; otherwise device/package, cooling or device-count changes are necessary. No part replacement or four-device 60 A approval is implied by keeping them in this study.

The fixed power connectors have four 1 mm holes per rail and unknown MPNs. At 60 A, perfect sharing still requires **15 A per contact**, or 20 A each if one contact opens. The single 2 mm input termination on each rail carries the full current. Hole size, extra layers and a successful resistance calculation do not establish a connector/wire/solder rating. Nominal fixed rings are 0.25 mm and need acceptance for the eventual copper/plating process. [Termination/thermal screen](thermal/preliminary-60A-review.md), [fabrication constraints](stackup/fabrication-capabilities.md).

Both source-to-drain banks conduct forward through body diodes before gate enhancement. This draft does not regulate inrush, provide a positive-input OFF/overvoltage disconnect, limit short-circuit current or provide MOSFET thermal shutdown. The front driver's approximately 21.7 ms nominal estimate is time to driver enable, not guaranteed full enhancement. Missing external capacitance/ESR, source impedance, harness inductance and load startup behavior prevent a defensible peak-inrush or SOA conclusion.

The earlier 6S envelope permits −25.2 V reversal and a charged +25.2 V output, hence a 50.4 V front-device differential before transient effects. A 25 V title alone does not reduce this fault case. NCV requires protection from raw −25.2 V because its DC input/source limit is −18 V. MID clamp pulse capacity and hot-reversal waveforms are unqualified. Optional zeners are DNP and cannot be credited as assembled protection. [Controller/fault audit](thermal/controller-and-fault-limits.md).

**Balance protection is incomplete.** J1 and TP1–TP7 remain intentionally open. Raw tap reconnection can bypass both positive-side banks; connected balance G plus reversed main return can form a pack-short path, and cell taps can back-power receiving electronics. DXF geometry defines neither receiver tolerances nor balancing current or safe fault behavior. Four versus six main MOSFETs does not resolve this interface.

## Required inputs and completion gates

The previous **45 A through this PCB was confirmed**. The new request changes the target to 60 A; the following required questions remain unanswered and are not silently assumed:

1. Is 60 A continuous or peak; what peak duration, duty and actual positive/return path through this PCB are required?
2. What maximum ambient, enclosure, airflow, permitted cooling arrangement and junction/board-temperature targets apply?
3. What connector/contact, cable and termination MPNs, all-contacts-loaded ratings and upstream fuse/BMS fault-clearing characteristics apply?
4. Which fabricator/assembler will approve the physical stackup, minimum finished copper/barrel plating, fixed rings, controller gaps, mask and stencil?
5. Which BMS/charger/monitor receives the balance leads; what input/ground fault tolerance, balancing current and connection/miswire cases must be protected?

The 60 A continuous case, 60°C ambient illustration, 70 µm conductor and 25/35 µm plating cases are analytical assumptions only. They are not accepted design requirements or fabrication selections. User PC-access authorization does not answer these engineering questions.

After those inputs are established, complete the electrical/fault and coupled thermal design; obtain actual Saturn IPC-2152 results using the approved input/stackup assumptions; define conductor regions and controlled same-net layer transfers; route/refill; resolve the NCV rule/manufacturing conflict and silkscreen issues; and rerun native ERC/DRC/parity. Manufacturing and appropriate hardware current/temperature/startup/reversal tests remain separate from CAD checks. Until then the current files are an editable evaluation project, **not a routed or fabrication-ready 60 A design**.

## Placement and future Saturn inputs

[Applied-placement source study](placement/placement-feasibility.md), [candidate positions](placement/candidate-positions.json), [corridor diagram](placement/prospective-corridors.svg) and [planned Saturn run matrix](saturn-records/planned-run-matrix.md) complete this preliminary record. The placement study describes the initial two-layer geometry before root applied four-layer enablement and corrected the NCV exposed land. The latest native validation above governs the current board.
