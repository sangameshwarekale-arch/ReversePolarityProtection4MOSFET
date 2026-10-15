# Preliminary fabrication capabilities: four-layer 25 V / 60 A board

Checked 2026-10-15. Fixed outline: 44.52 × 41.51 mm. The actual fabricator has not been identified. This report screens candidate processes; it does not establish a 60 A current rating or authorize fabrication. Copper order is L1/L2/L3/L4. A capability limit is not evidence that every combination of copper, thickness, plating, finish, and via treatment is available.

## Candidate stackups and evidence status

| Candidate | Nominal board thickness | Evidence and status |
|---|---:|---|
| JLCPCB, 2/2/2/2 oz | 1.6 mm | A specific combination is stated in JLCPCB's older localized copper guide: four layers, 2 oz inner, 2 oz outer, 1.6 mm, JLC3313. The localized article is dated May 2025. **Current order and engineering confirmation required.** |
| JLCPCB, 2/2/2/2 oz | 2.0 mm | **Not established.** Current selectors expose thickness and copper options separately; that does not prove this combination. |
| JLCPCB, 3/2/2/3 or 4/2/2/4 oz | 1.6 or 2.0 mm | **Not a published standard four-layer offering.** Current English guidance limits heavier-than-2-oz outer options to two-layer FR4. Do not model these as an available JLC four-layer build. |
| PCBWay, 2/2/2/2 oz | 1.6 or 2.0 mm | **Quote and approved stackup required.** Copper and thickness fall within general published capabilities, but no exact matching stackup was retrieved. |
| PCBWay, 3/2/2/3 or 4/2/2/4 oz | 1.6 or 2.0 mm | **Quote and approved stackup required.** A credible heavy-copper candidate, with substantially larger etch and mask requirements. Availability of the complete combination is unconfirmed. |

JLCPCB's September 2026 English guide allows 1/2 oz standard outer copper and 0.5/1/2 oz inner copper subject to layer count and thickness, and directs customers to the actual order page. It lists 0.16 mm width/space for 2 oz. The more specific older localized combination above must therefore be rechecked. [JLCPCB current copper guide](https://jlcpcb.com/help/article/jlcpcb-copper-weight), [JLCPCB older localized combination](https://jlcpcb.com/de/help/article/jlcpcb-copper-weight).

PCBWay's stackup explainer describes a standard multilayer envelope of 4–14 layers, 0.4–3.0 mm, up to 4 oz outer and 2 oz inner. Its separate current capabilities page lists broader limits. These envelopes do not supply a physical stackup for this board. [PCBWay stackup explanation](https://www.pcbway.com/pcb_prototype/What_is_layer_stack_up.html).

**Physical stackup limitation:** JLCPCB's retrieved impedance page displayed the default 1 oz outer / 0.5 oz inner stackup despite showing copper selectors. Its default JLC04161H-3313 dielectric dimensions must not be reused for 2/2/2/2 oz. No approved core/prepreg dimensions for an all-2-oz build were obtained. PCBWay provides a searchable stackup catalogue, but a matching heavy-copper drawing was not retrieved. [JLCPCB stackup selector](https://jlcpcb.com/impedance), [PCBWay official catalogue instructions](https://www.pcbway.com/blog/12/How_to_Choose_the_Stackup_for_Your_Needs_efcad645.html).

## Published process facts

### JLCPCB

The following are capability-page values, not contractual guarantees for an unquoted combination:

| Item | Published value |
|---|---|
| Finished thickness | 1.6 and 2.0 mm among options; ±10% at ≥1.0 mm |
| Average hole copper | **18 µm** |
| PTH hole tolerance | +0.13 / −0.08 mm |
| Hole position tolerance | ±0.075 mm |
| PTH annular ring at 2 oz | ≥0.254 mm |
| Inner via-hole / component-hole to copper | 0.20 / 0.30 mm |
| Via-hole / PTH-hole to trace | 0.20 / 0.28 mm; PTH 0.35 mm recommended |
| Routed copper edge clearance | ≥0.20 mm |
| Regular routed outline tolerance | ±0.20 mm |

Thus neither **25 µm minimum** nor **35 µm minimum** barrel plating is supported by the standard published 18 µm average. Ask engineering for a guaranteed minimum and acceptance method; otherwise calculations must reflect the actual lower bound. [JLCPCB rigid PCB capabilities](https://jlcpcb.com/capabilities/pcb-).

JLCPCB's official mask article reports multilayer LDI alignment within ±0.02 mm and 1:1 pad openings, and requires ≥0.20 mm pad spacing for a dam with 2 oz copper. Treat the alignment number as a published process claim requiring confirmation if used in a tolerance stack. [JLCPCB solder-mask design](https://jlcpcb.com/blog/basic-design-of-solder-mask).

### PCBWay

| Item | Published value |
|---|---|
| Outer / inner copper envelope | 1–8 oz / 1–4 oz; inner stated for 4–10 layers |
| PTH finished-hole envelope / tolerance | 0.15–6.0 mm / ±0.08 mm |
| Hole position tolerance | ±0.075 mm normal |
| Through-hole copper | 18–25 µm normal; 30–50 µm medium difficulty |
| Normal inner width/space at 2 oz | 6/8 mil = 0.1524/0.2032 mm |
| Normal outer width/space at 2 oz | 7/8 mil = 0.1778/0.2032 mm |
| Normal outer width/space at 3 oz | 10/12 mil = 0.2540/0.3048 mm |
| Normal outer via ring, 2 / 3 oz | 7 / 8 mil = 0.1778 / 0.2032 mm |
| Normal outer component-hole ring, 2 / 3 oz | 12 / 14 mil = 0.3048 / 0.3556 mm |

A 25 µm **minimum** is not guaranteed by an 18–25 µm range. A 35 µm **minimum** requires a special requirement even though 35 lies inside the 30–50 µm capability range. [PCBWay capabilities](https://www.pcbway.com/capabilities.html).

PCBWay's tolerance table lists normal outer width/space of 0.25 mm and normal via/component ring widths of 0.18/0.23 mm at 4 oz. Its other capability table is more restrictive for some 2/3 oz features. Use the more restrictive applicable rule pending engineering review; do not mix minima from different process columns. The tolerance table recommends 0.30 mm profile-to-copper. [PCBWay manufacturing tolerances](https://www.pcbway.com/pcb_prototype/PCB_Manufacturing_tolerances.html).

For ordinary colored mask, PCBWay lists minimum pad spacing of 0.20 mm at 2 oz and 0.25 mm at 3 oz; white/black 3 oz requires 0.30 mm and matte black 0.35 mm. Suggested Gerber expansion is 2–4 mil per side. No numerical PCBWay mask-registration tolerance was established from a primary process specification. **Expansion is not registration tolerance.** The selected mask, actual dam width and 4 oz rules need written confirmation. [PCBWay solder mask](https://www.pcbway.com/pcb_prototype/PCB_Solder_mask.html).

## Finished holes 0.4 / 0.5 / 0.6 mm

All three are inside both vendors' general hole envelopes. The complete heavy-copper/plating combination remains unconfirmed. Explicitly label the drawing and drill notes **FINISHED PTH DIAMETER**; the fabricator compensates the production drill for plating.

| Requested finished hole | JLC published acceptance range | PCBWay published acceptance range | Proposed via pad with 0.30 mm nominal ring |
|---:|---:|---:|---:|
| 0.40 mm | 0.32–0.53 mm | 0.32–0.48 mm | 1.00 mm |
| 0.50 mm | 0.42–0.63 mm | 0.42–0.58 mm | 1.10 mm |
| 0.60 mm | 0.52–0.73 mm | 0.52–0.68 mm | 1.20 mm |

Ranges are arithmetic from the cited tolerances; pad sizes are engineering proposals, not vendor quotes. They must be reviewed against fabrication drill oversize, hole position, layer registration, etch loss and residual-annular-ring criteria. A component terminal's annular ring must use the applicable component-hole rule, which can be larger than the via rule.

At fixed finished hole and barrel thickness, a 2.0 mm barrel is 25% longer than a 1.6 mm barrel. Its ideal resistance and Joule loss are therefore 25% higher for the same current. Increasing board thickness does not increase barrel conductance.

For electrical sensitivity calculations only, barrel cross-section is A = π × t × (D_finished + t), with dimensions in mm. This excludes fill material and has no via current-rating implication:

| Finished hole | A at 25 µm plating (mm²) | A at 35 µm plating (mm²) |
|---:|---:|---:|
| 0.40 mm | 0.03338 | 0.04783 |
| 0.50 mm | 0.04123 | 0.05883 |
| 0.60 mm | 0.04909 | 0.06982 |

Use minimum guaranteed plating, minimum finished diameter, the actual barrel length and temperature-dependent copper resistivity for the final electrical model. Thermal current capability still requires the actual via array, connected copper and cooling conditions.

## Via fill and soldering constraints

JLCPCB distinguishes soldermask plugging from epoxy/copper-paste fill plus a plated cap. Mask plugging is not a flat solderable VIPPO surface. Its general capabilities specify plugged-via separation ≥0.35 mm from mask openings and a 0.5 mm diameter maximum, versus 0.15–0.55 mm compatible diameter for filled/capped processing. Consequently, a 0.60 mm via in an SMT solder pad is **not established** by this offering. Ask which diameter definition applies and whether the requested four-layer heavy-copper board is accepted. [JLCPCB via covering](https://jlcpcb.com/help/article/pcb-via-covering), [JLCPCB capabilities](https://jlcpcb.com/capabilities/pcb-).

PCBWay describes IPC-4761 Type VII as filled and copper capped, using nonconductive epoxy plus copper plating/planarization. Ordinary tenting, partial plugging and fully filled/capped vias are distinct requests. Specify the required type and planarity for any via under a MOSFET thermal pad. Do not count nonconductive epoxy as added electrical copper cross-section. [PCBWay via covering](https://www.pcbway.com/pcb_prototype/PCB_Via_Covering.html).

Large planes and power packages create an uneven reflow thermal load. JLCPCB's assembly guidance recommends profiling a populated trial board using thermocouples and tuning soak/conveyor conditions to the actual thermal mass. This is an assembly-process constraint, not a reason to place narrow relief spokes in a 60 A path without recalculating them. Require the assembler to approve the solderable pad design, fill/cap treatment, stencil and process profile. [JLCPCB reflow profiling](https://jlcpcb.com/blog/reflow-soldering-profile-explained).

## Proposed fabrication-confirmation request

Request an engineering-approved quote for a routed 44.52 × 41.51 mm, four-layer FR4 board, first for **2/2/2/2 oz at 1.6 mm**, then compare **3/2/2/3 and 4/2/2/4 oz**, each at 1.6 and 2.0 mm. Ask for:

1. A numbered physical stackup: laminate and Tg, core/prepreg types and compressed thicknesses, final copper on every layer, finished thickness and tolerances. Nominal oz values and minimum guaranteed finished copper must be distinguished.
2. Finished PTH diameters 0.4/0.5/0.6 mm, production drill compensation, guaranteed minimum barrel copper at **25 µm** and separately **35 µm**, and microsection/coupon acceptance criteria.
3. Trace/space, annular ring, drill/registration tolerances, all-layer antipads, copper-to-route clearance, selected-mask alignment/expansion and minimum actual dam width for that exact build.
4. Via treatment outside pads versus Type VII fill/cap under pads, available hole diameters, cap copper and planarity; ask for conductive-fill material properties only if that process is requested.
5. SMT acceptance of the thermal/current pad geometry and a measured first-article reflow profile.

These are technical confirmation items, not an order or an external message. No fabrication request has been sent. No PCB layout or UI changes were made for this research.
