# Output-terminal candidates for the 24 V nominal / 25.2 V maximum / 45 A redesign

Research checked 2026-10-15 using official manufacturer sources. This is placement-input research only. It does not approve a 45 A assembled-board rating, change the circuit, or authorize routing. Existing J2/J3 remain in place with unknown current ratings; they are not certified as full-current outputs by this work.

## Placement recommendation

Reserve two single **Würth Elektronik 7466205R** M5 REDCUBE SMT blind-thread terminals: J4 on VOUT and J5 on GND. The manufacturer lists 70 A, a nominal cylindrical body diameter 9 mm and height 7 mm, and a single solid circular solder land diameter 10 mm without a locating-pin hole. The copper pad must remain a single electrical terminal; its bare-part courtyard is separate from the cable-lug and tool envelope. [7466205R official datasheet, page 1](https://www.we-online.com/components/products/datasheet/7466205R.pdf).

For initial placement use a **circular 11 mm diameter engineering courtyard**, centered on the solder land. This is an engineering reservation, not a manufacturer-specified courtyard or a proof of edge clearance. It gives 0.5 mm nominal radial clearance beyond the 10 mm pad. Do not use the empty corners of an 11 × 11 mm bounding box as a reason to reject a circular terminal at a curved board edge. Check the actual circular pad and component against the outline and all neighbouring objects.

The proposed lower-lobe centres supplied by the placement agent are J5 around (115.5, 107.2) and J4 around (138.3, 107.2) mm. These positions have not been geometrically certified by this research. They must be checked against the preserved outline, existing connector row, wire exit, driver access and top/bottom component envelopes.

## Compact and higher-margin alternatives

| Manufacturer part | Thread / nominal body | Official copper land and hole | Published current | Torque | Placement courtyard proposal |
|---|---|---|---|---:|---|
| 7466203R | M3 blind; diameter 7 × height 7 mm | Solid circle diameter 8 mm; no drill | 50 A maximum at 20 °C | 0.5 N·m | Circle diameter 9 mm |
| 7466204R | M4 blind; diameter 7 × height 7 mm | Solid circle diameter 8 mm; no drill | 50 A maximum at 20 °C | 1.2 N·m | Circle diameter 9 mm |
| **7466205R** | **M5 blind; diameter 9 × height 7 mm** | **Solid circle diameter 10 mm; no drill** | **70 A listed; this revision does not state a test temperature beside the rating** | **2.2 N·m** | **Circle diameter 11 mm** |
| 7466003R | M3 through-thread; diameter 7 mm; above-board body height 5 mm, overall 6 mm | Diameter 8.5 mm annular land around diameter 4.2 mm NPTH | 50 A maximum at 20 °C | 0.5 N·m | Circle diameter 9.5 mm; bottom boss/screw keepout needed |
| 74660013 reverse type | M3; diameter 10 mm flange; dimensions 3/5.6 mm in section | Diameter 11 mm annular land around diameter 7.3 mm NPTH | 85 A maximum at 20 °C | 0.5 N·m | At least diameter 12 mm plus opposite-side hardware |

All courtyard values in the final column are engineering proposals. Nominal dimensions are not individually specified maximum dimensions; the drawings invoke general DIN ISO 2768-1m tolerances. Confirm the supplier model and tolerance envelope before mechanical release. The 7466205R blind version has no pin; **7466105R is a different pinned part** and must not be assigned the same hole-free footprint.

Sources: [7466203R](https://www.we-online.com/components/products/datasheet/7466203R.pdf), [7466204R](https://www.we-online.com/components/products/datasheet/7466204R.pdf), [7466205R](https://www.we-online.com/components/products/datasheet/7466205R.pdf), [7466003R](https://www.we-online.com/components/products/datasheet/7466003R.pdf), [74660013](https://www.we-online.com/components/products/datasheet/74660013.pdf).

The M4 is a useful smaller alternative because an official 6 mm² M4 cable lug is available. The manufacturer's M3 tubular-lug catalogue contains 1.5/2.5 mm² choices, so the physically small M3 terminal does not by itself establish a suitable 45 A cable interface. The M5 has more nominal current margin and direct 6/10 mm² lug choices, at the cost of a larger pad and higher tightening torque. [Würth WA-CLUG catalogue](https://www.we-online.com/en/components/products/CLUG_TUBULAR_CABLE_LUGS).

For the native footprint candidate, assign the single electrical copper land **pad 1 at (0, 0)**. The selected terminal has no fixed electrical polarity; J4 pad 1 is assigned VOUT and J5 pad 1 GND by the schematic. The manufacturer's land-pattern drawing does not specify a solder-mask expansion value. Select that margin with the fabrication process, and do not treat the stencil diameter as a mask-opening diameter.

Official CAD links listed by the manufacturer are [KiCad WP-SMBU rev26b](https://www.we-online.com/components/products/download/KiCad_WP-SMBU%20%28rev26b%29.zip) and [7466205 STEP rev1](https://www.we-online.com/components/products/download/Downloads_STP_7466205%20%28rev1%29.stp). The catalogue links were retrieved, but their file contents could not be fetched through the available web tool; no claim is made that an official CAD model was imported or checked. The PDF's explicit dimensions support the placement reservation above.

## Cable-lug and access envelope

| Official lug | Screw / conductor | Overall dimensions relevant to reservation | Eye hole |
|---|---|---|---|
| 5580406 | M4 / 6 mm² | Width 10 mm; total length 21 mm | Diameter 4.3 mm |
| 5580506 | M5 / 6 mm² | Width 10 mm; total length 21 mm | Diameter 5.3 mm |
| 5580510 | M5 / 10 mm² | Width 12 mm; total length 22 mm | Diameter 5.3 mm |

These are wire-termination geometries, not ampacity guarantees for an arbitrary cable insulation, installation or ambient. Exact hole-centre-to-barrel placement must follow the lug drawing; total length must not be interpreted as the distance from screw axis to cable end. [5580406](https://www.we-online.com/components/products/datasheet/5580406.pdf), [5580506](https://www.we-online.com/components/products/datasheet/5580506.pdf), [5580510](https://www.we-online.com/components/products/datasheet/5580510.pdf).

For the placement review:

- Point the lug/cable exits toward the lower board edge and reserve the actual cable bend radius outside the board. The 10–12 mm lug width exceeds the terminal body and may exceed a bare-part courtyard.
- Reserve vertical screw-driver access, screw head and washer diameter, lug thickness, insulation/boot space and the resulting assembly height. The 7 mm bare terminal height excludes all of these.
- Keep both-side small components out of any board-support, clamp or strain-relief contact region. No underside protrusion is required for the selected hole-free blind terminal, but the board still needs mechanical support against tightening and cable pull.
- Select screw length from actual thread engagement, lug/washer stack and blind-hole geometry. Do not bottom a screw or assume an arbitrary screw length from the 4 mm thread dimension alone.
- Treat 2.2 N·m as the selected M5 terminal's published torque limit, not a permitted external cable bending moment or PCB pull-force rating. Apply a controlled process; do not transfer breaking-force demonstrations from other REDCUBE parts to this board.

**Hardware recommendation status:** lug 5580506 is the concrete M5/6 mm² candidate; 5580510 is the M5/10 mm² alternative. No screw or washer part number/length is recommended by the retrieved terminal data. M5 screw, washer stack, contact finish and locking method remain selections to complete after the manufacturer confirms usable engagement and bottom clearance. Naming an arbitrary M5 screw would create a false approved assembly. The tool approach is along the vertical terminal axis at (0, 0); its required diameter and overhead height depend on that final hardware and driver. The diameter-11-mm bare-part courtyard is not a driver-access certification.

## Rating and derating limits

The manufacturer explicitly makes operating current dependent on PCB, cable lug and cable cross-section. Its REDCUBE design guide presents a derating example measured using **6 mm² cable and a PCB with 2 × 70 µm copper**. That is a test configuration, not the actual geometry of this 44.52 × 41.51 mm board, nor a per-part guarantee at the intended hot-board temperature. The guide also explains that lower-layer current transfer requires additional vias and that ordinary open vias in a solder pad can drain solder. [REDCUBE SMD Design Guide, page 11](https://www.we-online.com/components/media/o153698v410%20BCF_REDCUBESMDDesignGuide_EN.pdf).

No part-specific numerical current-vs-ambient curve has been verified here for 7466205R. The fact that 45 A is below 70 A is useful screening margin, not proof of 45 A continuous operation under the assembled PCB's cooling conditions. The 50 A options at 20 °C have little nominal margin and must not be represented as 45 A rated at elevated ambient without further evidence.

The terminal-to-lug joint and solder-to-PCB joint both contribute resistance. As a sensitivity calculation only, two equal terminal paths at 45 A would have:

| Assumed resistance per terminal path | Combined drop, VOUT + GND | Combined heating |
|---:|---:|---:|
| 50 µΩ | 4.5 mV | 0.2025 W |
| 100 µΩ | 9.0 mV | 0.4050 W |
| 250 µΩ | 22.5 mV | 1.0125 W |
| 500 µΩ | 45.0 mV | 2.0250 W |

Method: V = I × (2R), P = I² × (2R). These are arbitrary resistance cases, not measured or manufacturer-specified contact resistance. Final qualification needs four-wire resistance and steady-state temperature measurements using the actual screw, crimp, wire, board copper, mounting support, ambient and enclosure.

## Reflow, pad and stencil requirements

The selected M5 datasheet specifies 150 µm solder-paste thickness and suggests an aperture diameter 9.8 mm with 1 mm subdivision features. The exact aperture geometry must be taken from the drawing or official library; it has not been reconstructed from text into a native footprint by this research. Use separate F.Paste apertures rather than allowing an unchecked full-pad aperture to override the stencil design. [7466205R datasheet](https://www.we-online.com/components/products/datasheet/7466205R.pdf).

The REDCUBE design guide says the published pad geometry contributes to mechanical retention; enlarging the surrounding connected copper and adding appropriate vias can improve anchorage. Alignment/screw holes in the through-thread/pinned variants must be NPTH. Do not add a conductive plated hole to a hole-free terminal merely to resemble a conventional screw terminal. [REDCUBE SMD Design Guide, page 7](https://www.we-online.com/components/media/o153698v410%20BCF_REDCUBESMDDesignGuide_EN.pdf).

For the smaller M4, the datasheet specifies reflow, not wave soldering, and a 150–200 °C preheat for 60–120 seconds, with a maximum ramp-up of 3 °C/s and 60–150 seconds above 217 °C. These are classification limits rather than a complete optimized production profile. The two-sided assembly sequence must be approved with the heavy terminals and MOSFETs supported; use the final part's own limits and a measured trial profile. [7466204R reflow/handling requirements](https://www.we-online.com/components/products/datasheet/7466204R.pdf).

## One two-pole connector versus two single terminals

A two-pole connector gives fixed polarity orientation and a common housing but requires its full body, mating and insertion-force envelope. A credible manufacturer-rated example is **Phoenix Contact MKDSP 10N/2-10.16, 1773976**, 76 A nominal, with a plan envelope **20.32 × 18.4 mm**, installed height 29.3 mm, 10.16 mm pitch and two solder pins per potential. It does not fit an approximately 10 mm deep lower strip without occupying more board area or altering connector positions. It uses wave soldering rather than the selected SMT terminal process. [Phoenix Contact 1773976 official data](https://www.phoenixcontact.com/en-us/products/printed-circuit-board-terminal-mkdsp-10n-2-1016-1773976).

Anderson's official PP45 PCB system is genuinely specified up to 45 A per pole, but the published PCB requirements include 2.3–3.8 mm board thickness and a 10-AWG-equivalent copper path; this is a significant compatibility conflict with the current 1.6/2.0 mm candidates. Its wire contacts, housings, staples and mating space must be treated as a complete assembly. It is not the current placement recommendation. [Anderson Powerpole PP15/45 official datasheet](https://www.andersonpower.com/content/dam/app/ecommerce/product-pdfs/PP-Pak/ds-pp1545.pdf).

Keystone 7760 was screened and rejected: the manufacturer's own page rates it **15 A**, despite the M3 screw and substantial-looking body. Appearance and screw size cannot establish 45 A capability. [Keystone 7760 official page](https://www.keyelco.com/product.cfm/product_id/1083).

Two separate J4/J5 terminals fit the available lobes more flexibly and allow the power and ground copper to approach independently. They require clear permanent VOUT/GND identification and a physical lug/cable arrangement that prevents polarity confusion and tool interference. They remain full-current candidates pending thermal and mechanical validation.

## Lifecycle and procurement evidence

Würth's official current catalogue lists 7466203R, 7466204R and 7466205R as **Active**, with production active and an expected lifetime above ten years. It provides current datasheets, official KiCad libraries and 3D files. Stock/lead-time fields require login and were not available; no in-stock quantity or delivery date is claimed. [Würth official blind-thread product catalogue](https://www.we-online.com/en/components/products/WP-SMBU_BLIND-HOLE).

No account login, order, sample request or paid action was performed. No onsemi site access was attempted for this research. No project PCB, schematic, footprint library or component value was changed by this research.
