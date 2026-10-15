# Manufacturing spacing and footprint audit

Checked 2026-10-15. Scope: fixed 44.52 × 41.51 mm outline, four-layer candidates for a 25 V / 60 A protection circuit. This is a fabrication and assembly screen, not standards certification or a 60 A rating. It does not change the PCB. Copper order is L1/L2/L3/L4. The actual fabricator and approved stackup remain unspecified.

The controller footprints make **2 oz outer copper the most credible ordinary-process candidate**. A 3/2/2/3 or 4/2/2/4 oz build cannot be assumed compatible with the small intrinsic gaps. Even an all-2-oz board requires specific exceptions or process confirmation for the fixed PTH rings and corrected NCV exposed-pad spacing.

## Geometry used in this screen

| Feature | Nominal intrinsic copper gap or ring | Basis |
|---|---:|---|
| LM74500, adjacent DDF8 lands | 0.200 mm gap | 0.650 mm pitch minus 0.450 mm pad width |
| NCV68261, existing custom EP to side land | 0.220 mm gap | EP 0.90 × 1.60 mm; side pad centre 0.91 mm; radial pad length 0.48 mm |
| NCV68261, manufacturer-sized EP to side land | **0.195 mm gap** | Corrected EP 0.95 × 1.65 mm; 0.91 − 0.48/2 − 0.95/2 |
| NCV68261, neighbouring side lands | 0.300 mm gap | 0.650 mm pitch minus 0.350 mm pad width |
| LFPAK56E, adjacent gate/source land | 0.570 mm gap | Placement-agent measurement; intrinsic footprint geometry |
| Preserved component PTHs | **0.250 mm nominal ring** | Fixed pad/drill geometry; not a residual-ring guarantee |

These are local footprint limits. Moving the parts or widening the power pours cannot enlarge them. A route/zone clearance exception also cannot change a pad-to-pad gap.

## NCV68261: what the official drawing actually verifies

The official onsemi **511DW, Issue B, 15 June 2018, document 98AON79327G** drawing was downloaded from the official onsemi.cn document endpoint and visually inspected as a complete rendered page. The original onsemi.com download endpoint denied access. No further download attempt is needed: the official drawing and render are already cached for this audit. [onsemi 511DW drawing](https://www.onsemi.cn/download/package-drawing/pdf/511dw.pdf).

After rotating its recommended mounting footprint into the project's left/right-pad orientation, the drawing specifies:

| Land-pattern dimension | Official recommended mounting footprint | Earlier custom footprint |
|---|---:|---:|
| Side lands, radial × pitch direction | 0.48 × 0.35 mm | Same bounding dimensions |
| Side-land pitch | 0.65 mm | Same |
| Overall span across both land columns | 2.30 mm | Same |
| Side-land column centres, calculated | ±0.91 mm | Same |
| Central exposed-pad land | **0.95 × 1.65 mm** | **0.90 × 1.60 mm** |

The earlier EP matches the nominal package metal dimensions E2/D2 rather than the recommended mounting-land dimensions. It is 0.05 mm smaller in each direction. Therefore the earlier description claiming conformity to the recommended mounting footprint was not supported. The root task is correcting the working four-MOSFET footprint and embedded pad dimensions; original backups and the separate six-MOSFET design remain reference records.

Dimensional verification is limited to the drawing and orientation. A matching bounding box does not establish the acceptability of roundrect corners, paste volume, mask openings, via treatment, solder joints or assembly yield. The NCV68261 datasheet's pin table identifies 1=S, 2=G, 3=D, 4=EN, 5=GND and 6=IN; the thermal pad is drawn but omitted from that pin-function table. [NCV68261 datasheet, pages 1–2](https://www.onsemi.com/download/data-sheet/pdf/ncv68261-d.pdf).

The working board's pad-7-to-GND convention has separate manufacturer support: the project's existing README records the previously verified official evaluation schematic, where U1.5 and U1.7 share GND. The current attachment therefore follows an official evaluation-design precedent; it is not an unverified inference from the package drawing, nor an explicit pad-7 instruction in the datasheet pin-function table. This supports the ground connection without certifying the complete custom footprint or assembly process. [onsemi official evaluation schematic](https://www.onsemi.com/download/eval-board-schematic/pdf/ncv68261mtwaitbg-gevb_schematic.pdf). This correction uses existing project evidence and the prior verification; no additional onsemi fetch was made.

## Comparison with candidate processes

JLCPCB's current copper guide specifies 0.16 mm width/space at 2 oz. Its capabilities list 2 oz PTH rings ≥0.254 mm and 2 oz minimum pad spacing of 0.20 mm for mask dams. Heavier outer copper is not a published standard four-layer option. [JLCPCB copper guide](https://jlcpcb.com/help/article/jlcpcb-copper-weight), [JLCPCB capabilities](https://jlcpcb.com/capabilities/pcb-).

PCBWay's capability table distinguishes normal and medium-difficulty processes. At 2 oz, normal outer spacing is 8 mil (0.2032 mm), medium 7 mil (0.1778 mm). At 3 oz, normal is 12 mil (0.3048 mm), medium 10 mil (0.2540 mm). Normal 2/3 oz component-hole rings are 12/14 mil (0.3048/0.3556 mm), medium 10/12 mil (0.2540/0.3048 mm). [PCBWay capabilities](https://www.pcbway.com/capabilities.html).

PCBWay's separate tolerance page lists normal 4 oz outer spacing 0.25 mm, and its most aggressive listed value 0.23 mm. This page is less restrictive than some entries in the capability table for other weights. It is not evidence that the complete desired stackup uses those limits simultaneously. [PCBWay manufacturing tolerances](https://www.pcbway.com/pcb_prototype/PCB_Manufacturing_tolerances.html).

| Existing/corrected feature | JLC all-2-oz screen | PCBWay 2 oz outer | PCBWay 3 oz outer | PCBWay 4 oz outer |
|---|---|---|---|---|
| LM74500 gap 0.200 | Above 0.16 etch limit; exactly mask-dam threshold, no nominal headroom | 0.0032 below normal spacing; medium-process etch potentially feasible by quote | Below both cited normal and medium spacing | Below both cited spacing values |
| Corrected NCV EP gap 0.195 | Above 0.16 etch limit; below 0.20 mask-dam threshold | 0.0082 below normal spacing; medium-process etch potentially feasible by quote | Below both cited normal and medium spacing | Below both cited spacing values |
| NCV neighbouring lands 0.300 | Above cited etch/dam limits | Above cited normal etch spacing | 0.0048 below normal; above medium spacing | Above cited 0.25 spacing |
| LFPAK56E gate/source 0.570 | Above cited local spacing limits | Above cited spacing limits | Above cited spacing limits | Above cited spacing limits |
| Fixed component-hole ring 0.250 | 0.004 below published 2 oz ring rule | Below normal and 0.004 below medium ring rule | Below cited component-hole rings | General 4 oz tolerance table alone does not establish ring acceptance for this build |

“Above a published limit” means this individual geometry passes that numerical screen. It does not mean that fabrication, a solder-mask dam, the complete stackup or assembly is approved. A failed ordinary-process screen is grounds for a specific engineering quote; it is not proof that no specialist process could produce the feature.

## Solder-mask slivers and registration

For two opposing copper edges with equal mask expansion e per side, the nominal mask strip is **W = copper gap − 2e**. Rounded corners do not remove the limiting straight-sided gap near the middle NCV land. Values below are geometry only:

| Copper gap | e = 0 | e = 0.030 mm | e = 0.0508 mm (2 mil) | e = 0.1016 mm (4 mil) |
|---:|---:|---:|---:|---:|
| LM74500: 0.200 mm | 0.2000 | 0.1400 | 0.0984 | −0.0032 |
| NCV corrected EP: 0.195 mm | 0.1950 | 0.1350 | 0.0934 | −0.0082 |
| NCV adjacent lands: 0.300 mm | 0.3000 | 0.2400 | 0.1984 | 0.0968 |
| LFPAK56E: 0.570 mm | 0.5700 | 0.5100 | 0.4684 | 0.3668 |

Negative entries mean overlapping mask openings; there is no strip. The read-only snapshot had board mask expansion zero and no local NCV/DDF8 override. Recheck the final native board and exported mask after the root's changes and vendor CAM processing.

JLCPCB reports multilayer LDI alignment within ±0.02 mm and permits 1:1 openings. This is a process claim, not zero registration error. Mask translation relative to copper can cover one pad edge and expose copper at another even when the nominal strip width is adequate. [JLCPCB mask design](https://jlcpcb.com/blog/basic-design-of-solder-mask).

PCBWay lists mask-pad spacing ≥0.20 mm for ordinary colored mask at 2 oz and ≥0.25 mm at 3 oz, with larger limits for some dark masks. It suggests 2–4 mil expansion. No numerical PCBWay registration tolerance was established here. A mathematical sliver must meet the selected process's actual minimum dam width after CAM; pad spacing, opening spacing, finished dam width and registration tolerance are different requirements. [PCBWay solder mask](https://www.pcbway.com/pcb_prototype/PCB_Solder_mask.html).

The corrected NCV EP gap does not satisfy either cited 0.20 mm 2 oz dam screen. A single underbody mask window or a specifically approved reduced-expansion process can be quoted. Removing a dam does **not** eliminate the copper etch spacing requirement, and it increases the need to control stencil volume and bridging during reflow.

## Exposed-pad stencil proposal

The earlier NCV pad had F.Paste at 1:1 with no reduction. Onsemi's general DFN/QFN guidance recommends approximately 70–80% centre-pad paste coverage for pitch ≥0.5 mm, with divided apertures. It also explains that an underbody mask web may be impossible and a single window may then require more careful solder control. These are assembly guidelines, not acceptance of this specific board. [onsemi AND9657, page 5](https://www.onsemi.com/download/application-notes/pdf/and9657-d.pdf), [onsemi SOLDERRM, DFN/QFN section, page 14](https://www.onsemi.com/pub/collateral/solderrm-d.pdf).

The root's proposed candidate is two F.Paste-only windows, each 0.80 × 0.70 mm, at (0, ±0.42 mm), with F.Paste removed from the full EP. Their combined area is 1.12 mm², 71.45% of the EP bounding rectangle 0.95 × 1.65 mm. With the existing 0.2 roundrect ratio, actual rounded copper area gives approximately 72.89%. Window-to-window steel web is 0.14 mm; rectangular edge insets are 0.075 mm horizontally and 0.055 mm vertically. Window corners remain inside that rounded EP. No obvious geometric flaw was identified.

**Status: engineering proposal only.** The assembler must approve stencil thickness, aperture shape, area release, paste alloy, mask window, board finish, oven profile and void/joint acceptance. Confirm that the full EP aperture is removed; otherwise it overlaps the proposed windows and restores excessive paste area.

## Fixed-hole ring tolerance

The 0.250 mm ring is nominal design geometry. It is not the minimum copper guaranteed after drilling and etching. An illustrative geometrical bound is:

**r_remaining = r_nominal − centre offset − half of positive finished-hole diameter error − pad-edge loss.**

For r_nominal = 0.250 mm, centre offset 0.075 mm and positive hole error 0.080 mm, the result is 0.135 mm before pad-edge loss. Using JLCPCB's +0.130 mm diameter limit gives 0.110 mm. This is an arithmetic illustration using published tolerances, not an IPC acceptance result or a reliable vendor process model. Production-drill oversize, finished-hole definition, copper at the hole mouth, inner-layer registration and the supplier's annular-ring acceptance convention must be resolved explicitly; do not double-count compensated drill oversize and finished-hole plating in the same model.

Since the pads and holes are mechanically fixed, obtain written acceptance of the exact geometry and residual-ring criterion for the selected copper/plating process. Choosing a smaller drill or enlarging a pad would change preserved geometry and is not assumed authorized by this audit.

## Electrical clearance and creepage at 25 V

Fabrication trace spacing answers whether copper can be etched reproducibly. Mask spacing answers whether ink can remain between openings and solder can be controlled. **Neither establishes electrical-insulation compliance.** Clearance is a path through air; creepage is a path along an insulating surface. Required distances depend on the applicable end-product standard, insulation function, actual working/transient voltage, pollution degree, material CTI and altitude. IEC 60664-1 supplies an insulation-coordination framework rather than a universal “25 V PCB gap” approval. [IEC 60664-1 scope](https://webstore.iec.ch/en/publication/59671), [TI explanation of clearance/creepage factors](https://www.ti.com/video/6146024211001).

Use a pairwise maximum-voltage matrix across normal operation, disabled/reverse conditions and credible transients. The NCV gate is charge-pumped above its source: its datasheet gives 9–15 V gate-to-source charged voltage for VIN ≥8 V. Thus a 25 V source can place approximately 40 V at the gate relative to ground within that numerical operating case; all controller gaps cannot be screened as merely 25 V. The EP is GND in the working netlist, making the gate-to-EP path relevant. This is a circuit-level inference, not an insulation rating. [NCV68261 datasheet, Table 7](https://www.onsemi.com/download/data-sheet/pdf/ncv68261-d.pdf).

No selected end-product insulation standard, contamination environment or qualified coating process has been supplied. This audit therefore gives no universal numerical electrical-clearance/creepage minimum and claims no IPC/IEC compliance. Ordinary LPI solder mask is not automatically a credited protective-coating system. The 60 A load changes heating and fault-energy consequences; it does not replace the voltage/environment analysis used to determine insulation spacing.

## Release conditions

Before fabrication, obtain a single approved process specification covering the exact stackup, all local footprint gaps, preserved PTH geometry, minimum copper/plating, selected mask, CAM openings and assembly stencil. At present, the credible route is an all-2-oz four-layer quote with explicit approval for the corrected NCV mask/etch geometry and fixed rings. Heavy outer-copper options require specific engineering acceptance of the intrinsic controller gaps or a reviewed package/layout change; their generic copper-weight availability is insufficient.
