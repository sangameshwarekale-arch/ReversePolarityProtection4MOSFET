# Saturn calculation plan — not executed

This is a planned run matrix. It contains **no actual Saturn output** and no selected conductor/via rating. The installed 8.47 calculator has no targetable window through the desktop interface. PC-access authorization was confirmed by the user; the failure is a tool/window limitation.

When access works and the missing requirements are established, use the exact approved stackup and guaranteed finished copper/plating. Record screenshots/export files plus every input and units. Prefer the installed help's recommended IPC-2152 without modifiers for its applicable conductor/via evaluations; use IPC-2221 only as a separately identified historical comparison. Do not call an extrapolated result hardware validation.

| Planned calculator | Inputs to compare | Output to record |
|---|---|---|
| External conductor | 60 A main, 30 A ideal branch, 15 A ideal contact; copper 70/105/140 µm candidates; ΔT 10/20/30°C; actual length; ambient cases 25/40/60°C | Required width or calculated capacity, resistance, drop, loss, all options/units |
| Internal conductor | 60/30 A, 70 µm candidate; actual layer dielectric/plane geometry and length; same ambient/ΔT comparisons | Width/capacity, plane/modifier settings and applicability limits |
| Parallel conductors/planes | Only verified SAME-NET parallel paths; actual bottlenecks, connected layers, plane distance/thickness | Sharing model, effective resistance and thermal model; no division by four merely for four layers |
| Through vias | Finished hole 0.4/0.5/0.6 mm; board 1.6/2.0 mm candidate; plating sensitivity 18/25/35 µm | Current estimate, height-effect/IPC settings, ΔT and resistance; distinguish 18 µm average from a guaranteed minimum |
| Via arrays | Actual available footprints, approved plated holes and spreading copper; candidate 20/30/40 counts only for comparison | Per-via current, computed capacity, ideal/unequal-sharing sensitivity and barrel/plane loss |
| Spacing/thermal tools where applicable | Maximum working/fault/transient voltage, environment and selected standard; actual material/geometry | Scope and assumptions; separate formal insulation or coupled thermal analysis where the tool does not provide it |

No numeric input above is an accepted operating limit or approved manufacturing selection. Planned units: mm, µm, A, V, mΩ, W and °C. Copper reference temperature and compensation settings must be recorded explicitly. Missing ambient/current-duty/fabricator information remains required before final runs.
