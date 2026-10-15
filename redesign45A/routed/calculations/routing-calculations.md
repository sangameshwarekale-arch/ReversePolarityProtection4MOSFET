# 24 V / 25.2 V maximum / 45 A routing calculations

**Routed engineering candidate; not qualified for45A operation or fabrication.** Measurements below come from the final saved KiCad filled polygons. Conditional calculations are separate from measured geometry. [Final native-file hash and checks](../reports/final-preservation-and-connectivity.json), [measurement source hash](../reports/measurement-source-hash.json).

## Actual CAD model and current path

The user confirmed45A passes this PCB. Positive current goes TP9 -> parallel Q1/Q2 -> MID -> parallel Q3/Q4 -> VOUT -> J4 and/or J3. The common return is J5/J2 -> GND -> TP8.45A is the sum of output branches. Four-pin legacy connectors and the incoming solder terminations have no verified manufacturer rating.

The saved provisional stack is1.6mm total: four70um copper layers, FR4 dielectric0.2/0.9/0.2mm and two10um masks, with ENIG specified. These are nominal CAD selections, not a vendor-approved physical stack or measured copper minimum. Four layers at70um are not four independent cooling surfaces. Power_45A_Target assigns VIN_RAW/MID/VOUT/GND; Gate_Control assigns the two buses, four gates, S_KELVIN and VCAP_A. Both use0.20mm clearance. Preferred editor widths are2mm for power and0.20mm for controls; they are not ampacity rules. Main load current uses the broad zones, not the0.20mm support branches.

There are195 track segments,100 through vias and14 filled zones. Power lands are solid connected. Twenty low-current component footprints use0.20mm local thermal gap/spokes for solderability. Zones use0.25mm different-net clearance and remove floating islands. Both front and rear carry VIN/MID power regions and ground return; two inner VOUT corridors carry output current across the board. Ground reference/return occupies the remaining regions on all layers. The fixed row and through-hole drills are included in the neck checks.

## Measured copper cross-sections

Native filled polygons were cut at0.025mm increments, including native clearance anti-pads. Physical via/PTH drill voids were subtracted even for same-net holes. Width is the sum of intervals within the stated path window; separated bands are not one uninterrupted trace. Full sampled intervals/windows are in [the measurement JSON](routed-copper-measurements.json).

| Section / layer | Minimum aggregate width mm | Cut position mm | Largest band at that cut mm |
|---|---:|---:|---:|
| VOUT transverse inner1 | 3.9808 | 124.200 | 3.1158 |
| VOUT transverse inner2 | 3.9808 | 124.200 | 3.1158 |
| VOUT upper-bank neck inner1 | 3.4500 | 88.400 | 3.2500 |
| VOUT upper-bank neck inner2 | 3.4500 | 88.400 | 3.2500 |
| VOUT terminal neck inner1 | 7.5988 | 100.300 | 1.5002 |
| VOUT terminal neck inner2 | 7.5988 | 100.300 | 1.5002 |
| MID upper bridge front | 3.3000 | 124.600 | 2.0500 |
| MID lower bridge front | 2.9573 | 124.650 | 2.2586 |
| GND left return rear | 4.1292 | 98.450 | 4.1292 |
| GND left return front | 1.6285 | 93.600 | 1.0289 |
| GND left return inner1 | 2.4553 | 91.750 | 2.4553 |
| GND left return inner2 | 2.4553 | 91.750 | 2.4553 |
| VIN lower branch front | 8.6005 | 90.800 | 4.1008 |
| VIN lower branch rear | 5.6858 | 92.975 | 2.4141 |

The VOUT transverse minimum is3.9808mm on each inner layer, versus7.6mm originally reserved before drilling/anti-pads. At assumed70um per layer, two identical minimum sections total0.5573mm²;45A divided by that area is80.7A/mm². This is a section-average illustration, not peak current density or ampacity. The upper VOUT neck's two3.45mm sections total0.483mm² at22.5A, about46.6A/mm². Ground's minimum same-cut sum over four layers is13.2144mm atY92.200, or0.9250mm² and48.65A/mm² at45A under an equal-potential assumption. Real sharing requires a3D electrical/thermal model or measurement.

## Resistance and voltage drop

Use R=rho L/A, rho20=1.724e-8 ohm m and rho(T)=rho20[1+0.00393(T-20)]. For varying widths, the optimistic slice model is R=rho integral(dx / sum(t*w(x))). It assumes equipotential cross-sections and ignores2D detours, contact spreading and unequal layer sharing.80C is a chosen copper-temperature example, not predicted board temperature.

| Inner path section | Assumed current A | Approximate R mOhm | Drop mV | Loss W |
|---|---:|---:|---:|---:|
| VOUT transverse | 45.0 | 0.32563 | 14.653 | 0.65940 |
| VOUT upper-bank neck | 22.5 | 0.15536 | 3.496 | 0.07865 |
| VOUT terminal neck | 45.0 | 0.04972 | 2.237 | 0.10068 |

These are partial path estimates. Do not add them to claim a guaranteed complete input-to-output resistance: source fingers, MID, ground, solder joints, terminations and3D transfers need a complete model. For an independently chosen20mV budget over14mm at45A/80C with two70um layers, uniform width per layer would be rho*L*I/(2*t*V)=approximately4.79mm. That solves a resistance budget only; it does not establish temperature rise.

## Via selection and loss examples

84 power/thermal vias are1.2mm land /0.6mm finished hole, nominal0.30mm annulus. Groups are9 at each downstream drain,20 near each output post,8 at each upstream source bank, and5 at each MID bank. They sit outside ordinary solder lands, with drill spacing checked.14 control vias are0.7/0.3mm; one D1 ground via is0.6/0.3mm. One0.55/0.25mm MID island tie at(126.9,89.0) is a **special via-in-pad requiring epoxy fill and copper capping on both sides**. It is not interchangeable with an open drilled hole. D3 remains DNP. This tie avoids a longer gate-bus detour; its process must be explicitly accepted by the fabricator/assembler.

Barrel area is pi[(d/2+p)^2-(d/2)^2], Rvia=rho*length/area and ideal array resistance is Rvia/N. The following stress examples use80C copper,1.76mm full barrel length and18um plating. JLCPCB publishes18um **average** plating, not a verified minimum for this board.25um cases are also in the CSV, explicitly assumed. Full-length models are conservative in vertical distance for inner-layer pickups but omit entry spreading; they are not a guaranteed overall bound. Equal current sharing is assumed.

| Array | Vias | Assumed group A | A/via | Ideal R mOhm | Ideal loss W |
|---|---:|---:|---:|---:|---:|
| Q3 /VOUT | 9 | 22.50 | 2.5000 | 0.11922 | 0.06035 |
| Q4 /VOUT | 9 | 22.50 | 2.5000 | 0.11922 | 0.06035 |
| J4 /VOUT | 20 | 45.00 | 2.2500 | 0.05365 | 0.10864 |
| J5 /GND | 20 | 45.00 | 2.2500 | 0.05365 | 0.10864 |
| Q1 /VIN_RAW | 8 | 22.50 | 2.8125 | 0.13412 | 0.06790 |
| Q2 /VIN_RAW | 8 | 22.50 | 2.8125 | 0.13412 | 0.06790 |
| Q1 /MID | 5 | 22.50 | 4.5000 | 0.21459 | 0.10864 |
| Q2 /MID | 5 | 22.50 | 4.5000 | 0.21459 | 0.10864 |

The MID/source examples assign an entire22.5A branch to that array as a screen; the actual front/rear split has not been solved. Via count was selected with geometry and ohmic screening, not an invented per-via ampacity rule. Thermal coupling, plating minimum and current crowding still require verification. Existing connector-hole barrels are not credited as the only layer-transfer path. [All plating/length/temperature cases](via-array-ohmic-examples.csv).

## Temperature-rise width screen and Saturn status

**No actual Saturn results are available.** The installed Saturn V8.47 launch did not return a targetable calculator window. None of the arithmetic here is described as Saturn output.

An additional independent arithmetic check uses the legacy IPC2221 fit documented by KiCad: I=k*deltaT^0.44*(Wmil*Hmil)^0.725, k0.048 external/0.024 internal. At70um and22.5A, it gives external uniform widths7.228mm for20C rise and4.746mm for40C rise. The10C result11.009mm exceeds the documented10mm width domain. The documented current limits are35A external and17.5A internal; **do not extrapolate it to45A or22.5A per inner plane**. It cannot validate this coupled multilayer/polygon board.11.25A internal examples are hypothetical comparisons, not the actual two-plane45A split. [Inputs/results](legacy-width-screen.csv), [official KiCad formula/domain reference](https://docs.kicad.org/5.1/en/pcb_calculator/pcb_calculator.pdf).

## MOSFETs, gate drive and complete thermal requirement

All four transistors and values are unchanged. For matched devices per bank, Rbank=Rdevice/2 and each loss=(45/2)^2*Rdevice. Front quoted maxima are1.2mOhm at25C/10V gate,2.2mOhm at105C/10V,2.8mOhm at175C/10V. Downstream maxima used are2.4mOhm at25C/4.5V and4.9mOhm at150C/4.5V, with25A datasheet tests. The resulting four-device screens are3.645W/81mV cold,7.189W/159.75mV mixed hot and7.796W/173.25mV at the higher quoted points. These are conditional test-point calculations, not equilibrium temperatures or a universal worst case. Front gate enhancement of at least10V has not been established from a guaranteed loaded controller output. [Front official sheet](https://assets.nexperia.com/documents/data-sheet/PSMN1R3-80SSF.pdf), [downstream official sheet](https://assets.nexperia.com/documents/data-sheet/PSMN2R0-55YLH.pdf).

The mixed-hot downstream loss is2.4806W/device. An assumed60C ambient/125C junction target requires isolated thetaJA <=26.20C/W; a60/40 current split raises the hotter downstream loss to3.5721W and tightens that budget to18.20C/W. Real devices share board heat, so individual datasheet test-board thetaJA values cannot be assigned independently. Even the four MOSFETs plus only the modeled0.66W VOUT corridor exceed7.8W;65C available rise divided by that load is about8.3C/W before local junction rise and the remaining copper/connector loss. There is no evidence this enclosed-size PCB achieves that. Cooling/thermal simulation and controlled hardware tests are required before45A operation.

Individual10ohm gate resistors and local bleeds retain their connections. R14-to-U1 S_KELVIN is a distinct routed net; its MID pickup shares the bank copper, so zero common-source impedance is not established. C2 must retain>=333nF effective value under operating conditions; nominal1uF alone does not prove it. Optional15V zeners remain DNP and are not credited as a guaranteed gate clamp. Main body diodes conduct during startup: EN-off does not provide positive-polarity load isolation or controlled inrush. Hot reversal, fault energy, charger/backfeed and gate transients remain unqualified. The longer D1 clamp feed is not a validated low-inductance transient clamp.

R13 remains10k:25.2²/10000=63.504mW,64.145mW at-1% resistance. Its official part sheet lists0.125W at70C, so those are50.8/51.3% of that rating; local temperature derating still applies. [Exact Yageo part](https://www.yageogroup.com/component-documentation/download/specsheet/RC0805FR-0710KL).

## Mechanical, connector and release limits

J4/J5 use the local7466205R M5 footprint:9mm nominal body,7mm nominal height,10mm solid copper land, no drill,11mm engineering courtyard. The70A catalogue figure does not qualify this assembly. No paste apertures were fabricated from unverified text; official divided stencil geometry remains on hold. Lug, screw/washer, thread engagement, torque reaction, insulating supports and cable strain relief remain unresolved. The old input2mm holes/2.5mm lands do not establish a45A solder termination. A6mm² round conductor has equivalent copper diameter about2.76mm and cannot simply be assumed to pass a2mm hole. The four-pin headers would each require11.25A/contact under ideal45A sharing, or15A after one open; their actual models are unknown. [Terminal/source review](../../calculations/output-terminal-selection.md).

The preserved12 terminations have no physical courtyards. Copper clearances are checked, but body/wire/tool interference is not verified. Known rear component thickness screening remains1.4mm maximum before solder/clearance;2.05mm local cavity and3mm nominal stand-off were engineering reservations, not enclosure approval. Two-sided reflow and heavy front terminals need assembly planning. U1's0.195mm intrinsic EP gap uses a scoped0.19mm copper rule supported by the quoted0.15mm multilayer2oz etch capability. Default clearance remains0.20mm, and no DRC exclusions or ignored categories hide errors. This does not resolve the2oz mask-bridge/stencil issue or the legacy0.250mm component-PTH rings versus the cited0.254mm process figure. [Manufacturer input supplement](manufacturer-screening-evidence.md).

**J1/TP1-TP7 remain intentionally open: balance-lead reverse-polarity protection is not implemented.** Preserving the existing circuit conflicts with calling this a complete balance-reversal protector. Undefined BMS limits/balancing currents and wiring permutations cannot be certified by this layout. The current stage also adds no short-circuit/current limiter or qualified thermal shutdown. No manufacturing files are released until these functional, thermal, mechanical and process checks are resolved. The detailed baseline calculations remain available [here](../../calculations/engineering-review.md).
