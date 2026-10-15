Historical placement-phase review. Placement was subsequently approved and routed; current status is in ../routed/README.md.

# 45 A placement review: approval boundary and remaining holds

Audit date: 2026-10-15. Reviewed the [engineering screen](engineering-review.md), [placement proposal](../placement/placement-review.md), [geometry checks](../placement/native-validation-and-routing-hints.json) and [terminal research](output-terminal-selection.md). No native files changed.

The review correctly uses **24 V nominal, 25.2 V maximum, 45 A total**, labels 60 A reports historical and makes no complete 45 A or balance-protection claim. Its 36-part, all-front disk capture is a baseline, not the proposed 38-part placement with 18 rear parts. Current native reports must describe the actual saved proposal.

## Placement approval only

- [ ] Confirm preserved outline/fixed mechanics, four front MOSFETs, 18 rear parts and J4 VOUT/J5 GND positions.
- [ ] Review lug/cable exits, tool approach and underside support. Courtyards, the 12 mm tool projection and suggested 3 mm stand-off are reservations, not verified enclosure/harness clearances.
- [ ] Attach the saved proposal's hash and current ERC/DRC/connectivity results. Keep footprint errors and unrouted connections visible; earlier 60 A results are historical.
- [ ] Keep tracks/vias/zones absent until placement approval. That decision permits routing; it **does not** certify electrical functionality, manufacturing or 45 A operation.

## Technical qualification remains separate

| Hold | Evidence required before the applicable release |
|---|---|
| **Fabrication** | Approve a physical stack with minimum finished copper/plating and process tolerances. Four enabled layers are insufficient. Resolve **0.195 mm NCV EP spacing**, **0.200 mm DDF8 spacing** and **0.250 mm nominal PTH rings** with the vendor. The NCV gap fails the current 0.200 mm screen; do not hide it with an exclusion. Heavy copper needs specific spacing acceptance. |
| **Assembly** | Approve mask windows, stencil and two-sided reflow/support. NCV's proposed divided paste covers 71.45% of its rectangular EP. The new terminal footprint has **no F.Paste** pending verification of its manufacturer's 150 µm subdivided stencil. Resolve thermal vias and solder wicking. |
| **Terminations/mechanics** | Qualify incoming TP8/TP9, any used J2/J3 contacts, wires/lugs, screw engagement, strain relief and support. The 7466205R's 70 A label is not a hot-board rating. Its 7 mm nominal height excludes hardware/tool access. Check actual housings, tails, underside insulation and cooling-plate clearance. |
| **Power routing** | After placement approval, calculate final filled-copper necks, pad entry, layer transfers, anti-pads and sharing for **both VOUT and GND**. Outputs share 45 A total. No power-via count or routed copper capacity is yet qualified. |
| **Gate/thermal** | Verify front physical **VGS ≥10 V**, effective C2, local loops, current sharing and shared-board temperature under defined duty/ambient/cooling. TI VCAP thresholds do not guarantee that gate minimum. Check unchanged 10 kΩ R13's hot derating, C4 near Q4's drain and rear gate-resistor heating. |
| **Fault/balance** | Define load/source/harness/charger conditions and validate startup, SOA, clamps and reversal waveforms. No qualified inrush/current limit or thermal shutdown is present. **J1 and TP1–TP7 are open; balance protection is unimplemented.** Resolving that function needs specifications and a reviewed electrical change. |

**Saturn unavailable:** Toolkit 8.47 is installed/running, but no targetable calculator window is exposed. No inputs were entered and **no actual Saturn result exists**. The R=ρL/A CSVs are ohmic examples, not ampacity or temperature-rise validation. Historical IPC-2221 extrapolations are not Saturn/IPC-2152 results.

**Release boundary:** placement approval permits routing. Manufacturing release requires the approved process, checked routing and current native ERC/DRC/assembly outputs. A 45 A operating claim also requires electrical, thermal, connector and fault evidence. Neither placement approval nor zero ERC violations supplies those qualifications or the missing balance function.
