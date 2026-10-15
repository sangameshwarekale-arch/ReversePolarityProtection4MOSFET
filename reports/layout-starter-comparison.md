# KiCad 9 layout starter validation

Unrouted layout starter. Not for fabrication. No 45 A qualification.

- Original backup SHA-256 unchanged: `5e2ade5c0697987eb2b9448d461077e301d8765232bfa24ed1501fa3eac19166`.
- All 60 Edge.Cuts primitives match exactly after native save/reload (including arc midpoint coordinates and widths).
- All 12 fixed mechanical footprint locations, angles, layers, pad coordinates/sizes/drills/shapes remain exact; all are locked.
- Removed 13 original unassigned raw balance tracks in the new copy; no tracks or copper zones remain.
- All 36 schematic footprints are present, including DNP parts; additional electronics are outside the board and require placement.
- Physical pad net assignments and schematic UUID paths verified after native reload for F8 schematic updates.

| Reference | X (mm) | Y (mm) | Angle (deg) | Exact match | Locked |
|---|---:|---:|---:|---|---|
| TP8 | 116.448949 | 90.040094 | 0.000000 | Yes | Yes |
| TP5 | 129.225962 | 74.915075 | 0.000000 | Yes | Yes |
| TP1 | 119.225810 | 78.729070 | 0.000000 | Yes | Yes |
| TP9 | 137.250829 | 90.040094 | 0.000000 | Yes | Yes |
| J3 | 136.725810 | 100.290031 | 0.000000 | Yes | Yes |
| TP7 | 134.225988 | 78.803061 | 0.000000 | Yes | Yes |
| J2 | 109.225810 | 100.290031 | 0.000000 | Yes | Yes |
| TP3 | 124.225861 | 74.890081 | 0.000000 | Yes | Yes |
| TP2 | 121.725886 | 76.065062 | 0.000000 | Yes | Yes |
| TP4 | 126.725886 | 74.554064 | 0.000000 | Yes | Yes |
| J1 | 119.225810 | 100.290031 | 0.000000 | Yes | Yes |
| TP6 | 131.725861 | 76.115075 | 0.000000 | Yes | Yes |

Electrical/thermal/DRC qualification is not implied. The deliberately open balance interface and unidentified connector ratings remain design constraints.
