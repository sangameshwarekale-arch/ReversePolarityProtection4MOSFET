# Changes after placement approval

The user explicitly approved the two-sided placement and continuation to routing. The approved native placement snapshot and approval record remain under redesign45A. All38 approved positions/sides/angles remain unchanged.

- Routed the existing main-rail circuit using195 track segments,100 vias and14 filled zones on four copper layers. Ground return is a power path. Two inner VOUT corridors cross the fixed connector row through the same-net J3 region.
- Used84 dedicated1.2/0.6mm power/thermal vias,14 ordinary0.7/0.3mm control vias, one0.6/0.3mm D1 return via and one0.55/0.25mm special filled/capped MID tie. The last requires an explicitly agreed process; ordinary open-via substitution is unacceptable.
- Removed redundant long control ground ties, gave U2/C1 a short local return, and tied all remaining intended power/control nodes. D1's preserved placement still entails a longer unqualified clamp feed.
- Added pad-to-zone thermal overrides for20 low-current supports; main MOSFET and high-current termination lands use solid connections. No component value, footprint copper/pad geometry, original net or functional mode changed.
- Saved a provisional1.6mm, four70um-copper stack and ENIG finish, power/gate net classes, a narrowly scoped U1 intrinsic-land0.19mm rule and0.25mm minimum drill. No rule categories remain ignored and no DRC exclusions were added. Twelve missing original courtyards are now visible warnings.
- Updated revision E/status text and assembly reference positions. New J4/J5 and their local symbol/footprint/BOM entries are retained.

Release holds: actual minimum finished copper/plating and thermal environment; full3D current sharing and startup/hot-reversal tests; input/old connector ratings and usable cable attachment; M5 lug/hardware/support/strain relief; exact terminal paste stencil; one filled/capped via; U1 mask/stencil process; legacy PTH rings; unknown connector bodies/enclosure clearance and two-sided assembly process. Balance paths remain open and unprotected. No45A operating certification or manufacturing release is claimed.

Saturn was installed but did not expose a targetable calculator window. No actual Saturn results exist. The supplied electrical/thermal arithmetic and geometry measurements are labeled as independent methods.
