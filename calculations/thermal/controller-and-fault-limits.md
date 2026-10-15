# Controller operation and fault limits — 25 V / 60 A draft

15 October 2026. **Analytical review only; not production qualification.** This review uses the current saved four-device BOM/netlist, the preliminary 60 A review, and official datasheet content retrieved earlier in this conversation. No PCB mutation, new onsemi network access, Saturn execution, load simulation or hardware test was performed. Unsaved editor changes are outside this review.

The gate-drive architecture is plausible for static main-lead reverse protection, but it does not establish safe 60 A startup, hot plugging, short circuits or reversal with connected balance leads. The thermal report already identifies 12.78 W in the mixed hot MOSFET-resistance case, excluding copper and contacts. Required duty, load capacitance, ambient/cooling, connector and fabrication information remains pending.

## Saved circuit and controller roles

Q1/Q2 sources are VIN_RAW and drains MID; Q3/Q4 sources are MID and drains VOUT. These are two parallel banks in series, both with body diodes pointing toward VOUT. U2 LM74500-Q1 has SOURCE/EN on VIN_RAW, GND on return, VCAP through C2 to VIN_RAW and GATE through individual 10 Ω resistors to Q1/Q2. U1 NCV68261 has IN/EN on MID, D on GND, G through two individual 10 Ω resistors, and S through R14 to MID. R14 carries source-reference/gate-drive currents, not the 60 A load path. Its saved net is correctly separated as S_KELVIN.

D grounded selects NCV reverse-polarity-only operation. Both EN pins are tied high with their supplies, so this implementation has no independent enable control. It also permits reverse current while enhanced, potentially needed for charging, but provides no positive-input OFF isolation. A depleted or overvoltage battery can still feed the load through forward body diodes after gate disable. This is not an undervoltage disconnect, overvoltage disconnect, charger, current limiter or thermal protector. [onsemi NCV68261, Rev. 1, Tables 1/9 and operation description](https://www.onsemi.com/download/data-sheet/pdf/ncv68261-d.pdf)

## Gate drive and charge

| Bank | Quoted gate/capacitance information | Engineering implication |
|---|---|---|
| Front: two PSMN1R3-80SSF | Resistance characterized at 10 V; ±20 V MOS gate limit; each CISS maximum 16.647 nF and Qg maximum 246 nC at the published test point | Need measured adequate gate enhancement and controlled transients; threshold voltage is not full enhancement. Total maximum quoted CISS is 33.294 nF. |
| Downstream: two PSMN2R0-55YLH | Resistance characterized at 4.5 V; ±20 V gate limit; each Qg typical/max 119/184 nC at 10 V, CISS maximum 11.353 nF | NCV's minimum charged drive of 9 V for VIN ≥8 V supports the lower-voltage resistance characterization. Published gate data are sizing points, not startup waveforms at 30 A/device. |

Manufacturer data: [front MOSFET Table 7](https://assets.nexperia.com/documents/data-sheet/PSMN1R3-80SSF.pdf), [downstream MOSFET Table 7](https://assets.nexperia.com/documents/data-sheet/PSMN2R0-55YLH.pdf).

TI recommends effective VCAP capacitance at least 10× driven CISS, with a 100 nF minimum. For the pair this gives **at least 333 nF effective**. C2 is 1 µF nominal X7R, but bias, tolerance, temperature and aging must be verified. Its capacitance is between VCAP and SOURCE, so the charge-pump differential is the relevant bias. Using nominal C2 and TI's typical 6.5 V release/300 µA equation gives approximately **21.7 ms to driver enable**. This is not the time to guaranteed 10 V gate drive: the pump continues raising its voltage afterward, and gate charge/bleeds alter the waveform. [TI LM74500-Q1, charge-pump and capacitor sections](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf)

**Front enhancement remains a qualification condition.** Inspection of the local TI Table 6.5 shows no explicit guaranteed fully charged GATE-to-SOURCE minimum. The minimum 10.3 V pump turn-on and 11 V pump turn-off values describe VCAP-to-SOURCE thresholds, not a loaded MOSFET-gate voltage guarantee. At SOURCE=3.2 V and VCAP load ≤30 µA, the separate VCAP minimum is 8 V. This does not prove 10 V gate drive across the whole supply range. At a normal 6S voltage, adequate drive is expected, but the actual gate minimum after driver/trace drops, bleeds, temperature and supply variation still needs evidence. Therefore the front 1.2/2.2/2.8 mΩ values and resulting thermal/loss tables are **conditional on establishing at least 10 V at each front gate**. They are not guaranteed circuit-level maxima. A final selection must either prove this condition over the intended envelope or use resistance characterized at a suitably lower guaranteed gate drive. [TI electrical-characteristics table](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf)

For downstream gates at 10 V, the two 1 MΩ bleeds draw 20 µA and the typical internal 1.1 MΩ path about 9.1 µA. At the NCV published 320 µA typical/170 µA minimum initial-charge test point, Q/(Icharge−Ibleed) estimates are **0.82 ms typical and 2.61 ms conservative test-point case**, using totals 238/368 nC. Neither is a guaranteed timing bound: charging current is specified initially at VGS=0 and a particular input/sense condition; actual current and nonlinear capacitance vary during turn-on. C5 is one optional common 1 nF gate-to-GND capacitor and is DNP. [onsemi Table 7](https://www.onsemi.com/download/data-sheet/pdf/ncv68261-d.pdf)

The controller gate pins drive capacitance, not the 60 A load. More parallel MOSFETs reduce conduction loss while increasing gate charge. Individual 10 Ω resistors help control ringing, but turn-off time, Kelvin-source bounce and maximum VGS still require measurements at both MOSFET banks.

## Startup and hot plugging: what can be calculated

Body diodes conduct as soon as a positive source can forward-bias the path, before either bank is fully enhanced. Therefore C5 or a slow gate rise cannot produce a controlled output ramp in this single-direction RPP topology. TI explicitly requires consideration of startup body-diode/inrush current. [TI startup guidance](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf)

Capacitor energy E=½CV² and charge Q=CΔV can be calculated once total effective capacitance and initial voltage are known. At 25.2 V, the nominal onboard C4=1 µF stores approximately **0.318 mJ**. A hypothetical 1 mF load stores 0.318 J; 10 mF stores 3.175 J. These examples are not measured load values and do not equal the energy dissipated in any particular MOSFET.

Without external load capacitance/ESR, initial voltage, load startup behavior, source impedance/current limit, harness inductance, connector bounce and operating temperature, there is no defensible inrush peak, diode pulse energy, voltage overshoot or SOA conclusion. Even a 60 A continuous request does not imply a 60 A startup peak. A conditional 60 A-from-time-zero, 1 V forward-drop example would dissipate 60 W in a diode bank during its ungated interval; the actual 30 A/device forward voltage is not bounded by the quoted 25 A diode test point. Use the measured/modelled ∫VDS(t)ID(t)dt and transient thermal impedance/SOA; do not treat nominal gate timing as a validated hot-plug limit.

## Static reverse connection and fast faults

With main leads reversed and balance disconnected, VIN_RAW becomes −25.2 V relative to board return. This is within LM74500's specified negative-input envelope. The front bank turns off and its body diodes block. If MID/VOUT retain +25.2 V from an output capacitor or charger, the front MOSFETs can see approximately **50.4 V**, motivating their 80 V selection. NCV itself has a **−18 V DC input/source limit** and therefore cannot be connected directly to the reversed raw pack. [TI ratings](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf), [onsemi Table 2](https://www.onsemi.com/download/data-sheet/pdf/ncv68261-d.pdf)

D1 is correctly oriented with anode at GND and cathode MID; R13 bleeds MID toward return. These assist with static leakage/floating nodes. They do not establish a hot-reversal clamp-energy capability. Before the front gates discharge, channel current and parasitic coupling can cause MID or gate-source excursions. Wiring inductance introduces L·di/dt voltage, and actual pulse energy depends on the missing source/load data. If a front MOSFET shorts, raw reversal can reach MID; this design is not demonstrated single-fault redundancy.

D2/D3 are optional 15 V zeners and are DNP. They cannot be credited with protection as assembled. Moreover, their nominal voltage is not a guaranteed peak clamp: the chosen 15 V type reaches 15.6 V at its reference current, while LM74500 GATE-to-SOURCE absolute maximum is 15 V. Ordinary zener forward conduction also does not guarantee the controllers' −0.3 V gate-source minimum. Population and transient clamp design require separate review; an optional footprint is not validation. [Nexperia zener Table 8](https://assets.nexperia.com/documents/data-sheet/BZT52H_SER.pdf), [TI absolute ratings](https://www.ti.com/lit/ds/symlink/lm74500-q1.pdf)

## Balance-connected reversal and release scope

The saved netlist leaves J1 and TP1–TP7 intentionally open; balance protection remains unimplemented. Direct raw G/B1–B6 reconnection would create paths outside the positive-side switches. If main leads are swapped while balance G is tied to receiving-electronics ground, actual pack− can be connected to actual pack+ through that ground conductor and the reversed main return. Neither bank interrupts this bypass. Raw B6 or intermediate taps can also back-power a receiver through supply or input clamps; permutations can violate individual cell-input limits.

A DXF cannot define receiver voltage tolerance, balance current, input clamping, ground isolation or fault-energy limits. Those specifications are required before completing the interface. Main supply reversal with balance disconnected, reversal while connected, and individual tap permutations must be treated as distinct fault cases.

Before production, establish duty/ambient/cooling and rated terminations/fabrication; define the receiver and balance fault envelope; qualify startup/reversal waveforms, gate drive, clamp pulse capacity and fuse/BMS clearing behavior; and complete coupled thermal/current-sharing verification. The current circuit has no short-circuit limiting or MOSFET thermal shutdown. ERC/DRC, a four-layer stackup or a Saturn conductor-width result cannot alone certify these fault conditions.

Scope conclusion: **the four-MOSFET draft remains a main-lead static RPP architecture awaiting dynamic, thermal, termination and balance-interface qualification.**
