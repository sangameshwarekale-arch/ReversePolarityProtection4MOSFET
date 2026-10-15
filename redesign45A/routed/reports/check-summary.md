# Final native KiCad9.0.7 results

| Check | Actual result |
|---|---:|
| ERC violations |0|
| DRC electrical/geometry errors |0|
| DRC warnings |12|
| Unconnected items |0|
| Schematic/PCB parity issues |0|
| Track segments / vias / filled zones |195 /100 /14|

All12 warnings are missing courtyards on the12 original connector/tap footprints. Five inherited ignored categories were enabled as warnings; there are no ignored rule categories or DRC exclusions. The required U1-specific0.19mm intrinsic pad-pair rule,0.20mm default clearance and0.25mm minimum drill are included in the native project/rules files. These are documented fabrication-screen choices, not suppressions of report entries.

The native CLI wrote the JSON reports and they were parsed. It also emitted sandbox warnings for unrelated user KiCad settings/telemetry/registry files; these are preserved in the CLI logs. Exit zero was not treated as proof without reading the report.

All36 old footprint identities/values/pad geometry/pad nets/paths and all39 original schematic instances are preserved. The60 outline primitives,12 fixed mechanical footprints and38 approved placements remain unchanged. Fresh XML exports retain all95 old pin/net nodes, adding onlyJ4.1 VOUT andJ5.1 GND. Local footprint libraries load natively. The77-file untouched backup and Desktop source still match intake hashes. See [machine-readable audit](final-preservation-and-connectivity.json).

DRC does not establish45A ampacity, thermal safety, transients, termination ratings, assembly process, body envelopes or balance functionality. Manufacturing remains on hold. No Gerber/drill files are provided.
