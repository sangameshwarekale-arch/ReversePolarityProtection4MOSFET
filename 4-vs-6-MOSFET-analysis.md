# Four versus six MOSFET engineering comparison — 15 October 2026

**Decision: four MOSFETs are a feasible architectural candidate using 2 upstream + 2 downstream. Neither four nor six has a qualified 45 A continuous board rating.**

The separate editable four-device project keeps the NCV68261 and LM74500-Q1 controllers and the existing exact board outline/mechanical footprints. It is an unrouted layout starter. The original six-device project and original backups remain unchanged.

## Assumptions and sources

45 A continuous load; equal sharing within each bank; fully enhanced gates. Calculations exclude copper, vias, contacts, terminations and controller dissipation. Elevated-temperature resistance cases use different published junction temperatures; they are sizing benchmarks, not a self-consistent thermal operating point.

- [PSMN1R3-80SSF datasheet](https://assets.nexperia.com/documents/data-sheet/PSMN1R3-80SSF.pdf): maximum Rds(on) 1.2 milliohm at25C, 2.2 milliohm at105C, 2.8 milliohm at175C; all at10V gate / 25A test current.
- [PSMN2R0-55YLH datasheet](https://assets.nexperia.com/documents/data-sheet/PSMN2R0-55YLH.pdf): maximum Rds(on) 2.4 milliohm at25C and4.9 milliohm at150C; both at4.5V gate /25A test current. The lower-drive specification is used conservatively despite the higher nominal NCV gate drive.
- [NCV68261 datasheet](https://www.onsemi.com/pdf/datasheet/ncv68261-d.pdf): continuous negative input/source limit -18V. It cannot directly face continuous -25.2V reversal. D-grounded RPP mode permits reverse charging current when enhanced.
- [LM74500-Q1 datasheet](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf): front reverse-polarity controller, charge-pump operation and capacitor sizing.

## Equations

For front count Na and downstream count Nb:

Rtotal = Ra/Na + Rb/Nb

Vdrop = I × Rtotal; Ptotal = I² × Rtotal

Current per front device = I/Na; current per downstream device = I/Nb

Pfront,each = (I/Na)² × Ra; Pdownstream,each = (I/Nb)² × Rb

## Calculated comparison

| Resistance case | Front + downstream | Total resistance (mΩ) | Drop at45A (mV) | MOSFET loss (W) | Front loss each (W) | Downstream loss each (W) |
|---|---:|---:|---:|---:|---:|---:|
| 25 C specified resistance | 2 + 4 | 1.200 | 54.00 | 2.430 | 0.607 | 0.304 |
| 25 C specified resistance | 2 + 2 | 1.800 | 81.00 | 3.645 | 0.607 | 1.215 |
| 25 C specified resistance | 1 + 3 | 2.000 | 90.00 | 4.050 | 2.430 | 0.540 |
| 25 C specified resistance | 3 + 1 | 2.800 | 126.00 | 5.670 | 0.270 | 4.860 |
| 105 C / 150 C benchmark | 2 + 4 | 2.325 | 104.62 | 4.708 | 1.114 | 0.620 |
| 105 C / 150 C benchmark | 2 + 2 | 3.550 | 159.75 | 7.189 | 1.114 | 2.481 |
| 105 C / 150 C benchmark | 1 + 3 | 3.833 | 172.50 | 7.763 | 4.455 | 1.103 |
| 105 C / 150 C benchmark | 3 + 1 | 5.633 | 253.50 | 11.407 | 0.495 | 9.922 |
| 175 C / 150 C screening | 2 + 4 | 2.625 | 118.12 | 5.316 | 1.417 | 0.620 |
| 175 C / 150 C screening | 2 + 2 | 3.850 | 173.25 | 7.796 | 1.417 | 2.481 |
| 175 C / 150 C screening | 1 + 3 | 4.433 | 199.50 | 8.978 | 5.670 | 1.103 |
| 175 C / 150 C screening | 3 + 1 | 5.833 | 262.50 | 11.812 | 0.630 | 9.922 |

For 2+2 at25C: Rtotal =1.2/2 +2.4/2 =1.8mΩ; drop=45×0.0018=0.081V; loss=2025×0.0018=3.645W. Each front device dissipates0.6075W and each downstream device1.215W. Reducing downstream count4→2 doubles downstream bank loss and quadruples the loss per remaining downstream device. The 2+2 allocation has the lowest loss among the four-device allocations with these same two MOSFET types.

## Thermal screening

Illustrative design assumptions only: ambient60C and target junction125C, allowable rise65C. A first-order isolated-device condition is effective Rtheta <= (Tj,target-Ta)/Pdevice. This is a screening requirement, not a claim about the actual board.

Using the175C/150C resistance screening values:

- Front each: P=(45/2)²×0.0028=1.4175W; required effective Rtheta <=65/1.4175=45.86C/W.
- Downstream each, four-device design: P=(45/2)²×0.0049=2.480625W; required effective Rtheta <=65/2.480625=26.20C/W.
- Downstream each, six-device design: P=(45/4)²×0.0049=0.620156W; corresponding requirement <=104.81C/W.

The downstream manufacturer examples are42C/W with25.4mm-square70um copper and85C/W with minimum footprint. These reference examples do not establish the needed26.2C/W in this irregular board. More cooling copper, thermal vias, thicker copper or a defined heat-removal path may be necessary. All devices heat the same board; mutual thermal coupling and copper/contact loss must be included. The resistance-temperature curve and thermal model must be solved consistently and confirmed by hardware temperature measurements. The175C resistance test point is not a recommended design operating temperature.

## Footprint and gate-drive tradeoff

Measured project courtyards: LFPAK88=9.30×9.10=84.63mm²; LFPAK56E=7.34×5.90=43.306mm². MOSFET courtyard sum decreases342.484→255.872mm², saving86.612mm² (25.3%). Four0603 gate/bleed resistors are also removed. This is a placement-envelope saving, not equivalent cooling-copper saving or proof of routing feasibility.

At the published10V gate-charge test points, downstream total typical charge halves476→238nC; maximum halves736→368nC. External1M gate bleeds draw20uA for two devices at10V, versus40uA for four. Reduced gate loading helps charging/discharging; exact timing depends on actual voltage/current/temperature and the controller pump characteristic. The front bank and C2 are unchanged; its nominal1uF capacitor still gives roughly21.7ms typical driver-enable delay. Body diodes can power the output before gates enhance, so neither variant supplies controlled soft start.

## Copper, contacts and imbalance

Every additional1mΩ of total copper/contact resistance adds45mV and2.025W at45A. Four paralleled connector contacts would each carry11.25A only with equal sharing; connector part/rating and contact resistance remain unknown. A narrow connector-pad neck may dominate heating even when MOSFET conduction loss is low.

Parallel devices do not guarantee exactly equal current. For a two-device bank with resistances R1/R2 (including branch copper), I1=I×R2/(R1+R2). If branches were1.0 and1.2mΩ, currents would be24.55 and20.45A. Symmetric routing and thermal conditions are needed; different gate thresholds also affect startup sharing.

## Voltage and transient checks

The front80V bank remains in place. A25.2V charged output facing a reversed25.2V battery can place about50.4V across a blocking path before transient overshoot. The downstream55V bank is intended to see protected MID and is not substituted on the raw reversed input. Voltage margins, gate-source limits, D1 clamp energy, hot-reversal waveforms and startup SOA remain unverified; count reduction alone does not settle them. A shorted front parallel MOSFET defeats that bank, so two banks are not established single-fault redundancy. There is no short-circuit current limiting, complete positive-overvoltage isolation or qualified thermal shutdown.

## Balance interface

MOSFET count does not protect arbitrary G/B1–B6 reversal/permutation. The DXF establishes geometry, not BMS input limits or fault-current paths. If the receiving electronics joins raw balance G to its main-power GND, reversed main leads can create a battery-short path through the balance ground conductor that the high-side power MOSFETs cannot interrupt. Other taps can back-power an unknown BMS through its internal paths. All fourteen drafted balance endpoints remain intentionally open; direct pass-through is not an approved protected solution.

## Qualification required before fabrication

Specify copper stackup and cooling/ambient, identify power connectors/terminations and BMS balance interface, design their protected current paths, verify startup/fault waveforms and semiconductor SOA, measure temperature rise at45A, and complete PCB placement/routing plus ERC/DRC. Four can be accepted only when these checks establish adequate margins; six does not remove these requirements.
