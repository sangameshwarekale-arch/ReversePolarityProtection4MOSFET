# Preliminary copper and via calculations — 15 October 2026

Status: independent analytical sensitivity study, not a physical 60 A qualification. Saturn has been launched but its calculator window is not exposed by the desktop-control interface; no Saturn result is claimed. Critical current-duty, ambient/cooling, connector and fabricator answers are pending.

## Track-width comparison

`tracks/independent-IPC2221-comparison.csv` uses I=k×ΔT^0.44×A^0.725 with A in square mils, k=0.048 external /0.024 internal; width=A/copper thickness. The coefficient/exponent method is described in [TI TIDUA53](https://www.ti.com/lit/ug/tidua53/tidua53.pdf). It is an older model and the60A outputs are extrapolations; they are not IPC-2152 results, design recommendations or proof of ampacity. Saturn's installed help recommends IPC-2152 without modifiers for most applications. IPC notes that [planes and parallel conductors require careful interpretation](https://www.ipc.org/system/files/technical_resource/E7%26S22_03.pdf). Layer currents cannot simply be divided by four without evaluating actual connectivity, widths and thermal coupling.

## Copper resistance and loss

`copper/rectangle-resistance-sensitivity.csv` uses R=ρ(T)L/(w×t×N), where N counts electrically identical SAME-NET parallel paths with identical geometry and equal sharing. ρ20=1.7241e-8 ohm-m and α=0.00393/C are representative annealed-copper engineering values, not measured board material. ρ(T)=ρ20[1+α(T−20C)]. Vdrop=IR, Ploss=I²R. Real zones require a current-distribution model accounting for holes, finite pad injection, corners, necks and unequal layer paths. The circuit's VIN_RAW, MID, VOUT and GND must remain separate.

Sheet resistance of70um copper at20C is0.2463mΩ/square; at80C it is0.3044mΩ/square. A20mm-long,10mm-wide70um rectangle on two perfectly parallel same-net layers has0.2463mΩ at20C,60A drop14.78mV and0.887W loss. This says nothing by itself about allowable temperature rise. At80C loss rises to approximately1.096W. Every additional1mΩ in the complete60A path adds60mV and3.6W.

## Via barrel and parallel arrays

`vias/barrel-array-ohmic-sensitivity.csv` uses annulus area A=πt(Dfinished+t), barrel R=ρL/A, ideal array R=Rvia/N. Finished-hole and plating dimensions are distinct; production drill compensation belongs to the fabricator. The18um column is only sensitivity to the published average, not a guaranteed minimum.25/35um columns require explicit fabrication guarantees. Resistance calculations do not establish a safe current per via. Solder/lead conduction, spreading resistance, thermal coupling, plating voids, hole tolerances and nonuniform current are excluded.

Example: finished0.6mm,25um plating,1.6mm length gives A=0.04909mm² and Rvia≈0.562mΩ at20C. Twenty ideal vias sharing60A carry3A each, array R≈0.0281mΩ, drop≈1.69mV and barrel loss≈0.101W. **3A is an assumed current split, not a qualified via rating.** A20-via array is not selected for fabrication. Saturn IPC-2152 evaluation and actual board/fabricator validation remain required. A longer2.0mm barrel increases resistance25%. Copper-less epoxy fill is not added electrical cross-section.

## Ring and process tolerances

The existing1.5mm pads/1mm holes and2.5mm pads/2mm holes have0.25mm nominal rings. JLC's published2oz PTH ring is≥0.254mm; PCBWay component-hole rules can be larger. Current footprints cannot be asserted compatible with a heavy-copper process without review. Larger copper lands may be possible while retaining centres/drills, but assembly/mechanical clearances must be verified.

For a proposed1.1mm via pad/0.5mm finished hole, nominal ring=(1.1−0.5)/2=0.30mm. A sensitivity using0.13mm positive hole tolerance,0.075mm position offset and0.025mm radial etch loss gives residual ring=(1.1−0.63)/2−0.075−0.025=0.135mm. These tolerance assumptions are not a vendor-approved acceptance stack and must not be combined blindly with capability minima. See `stackup/fabrication-capabilities.md` for sourced process limits.

## Four-layer topology proposal

Evaluate a1.6mm all-2oz build first, with copper weights/minimum finished thickness guaranteed by the selected vendor. No exact heavy-copper dielectric stack is approved yet. Do not use the vendor's1oz stack dimensions for2oz.

- L1: components, short source/drain power connections, gates and local bypass loops.
- L2: GND reference and main-return copper where appropriate. Return current capacity must be calculated; GND is not a substitute for positive power nets.
- L3: separate VIN_RAW, MID and VOUT power regions with same-net layer connections.
- L4: additional return/power regions on their correct nets, and limited signals if needed.

Use broad solid power-pad connections, multiple same-net stitching vias at controlled transfers, and avoid relief spokes/necks in the60A path. Do not route thermal drain vias into GND. MID/VOUT drain regions must not be shorted by a common metal heatsink. Wide copper may improve heat spreading but cannot establish the junction-to-ambient cooling needed in `thermal/preliminary-60A-review.md`.

## Spacing and qualification status

25V nominal alone is not the maximum differential voltage: reversed25.2V input and an already charged25.2V output can give50.4V before transients. Input maximum, transient envelope, pollution degree, altitude, coating and insulation category remain undefined.0.5mm between main power regions is a provisional engineering target, not a certified creepage/clearance calculation. Fine-pitch IC-pad exceptions need manufacturer land-pattern and fabricator confirmation; heavy copper may make the supplied NCV pattern unmanufacturable.

No final via count, finished stackup, temperature-rise limit, heatsink, power-connector rating or protected balance interface is approved. No ready-for-fabrication Gerbers or drill set is issued. The user must resolve these missing design inputs before a60A release can be justified.
