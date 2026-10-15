# 24 V / 25.2 V maximum /45 A target — routed evaluation, revision E

Open **ReversePolarityProtection4MOSFET.kicad_pro** in KiCad9. All CAD files are native/editable, with local symbol and footprint libraries and a matching .kicad_dru rules file. The PCB contains38 footprints,18 rear components,195 track segments,100 vias and14 filled zones. The original outline, fixed connectors and existing component values/connections are preserved.

**This is an engineering candidate, not qualified for45A operation or manufacture.** Final checks: ERC0; DRC0 errors and12 missing original-courtyard warnings;0 unconnected;0 schematic/PCB parity issues. No ignored DRC categories or exclusions hide those warnings.

Start with the [current routed review](redesign45A/routed/README.md), [comparison image](redesign45A/routed/images/routed-comparison.png), [calculation report](redesign45A/routed/calculations/routing-calculations.md), [check results](redesign45A/routed/reports/check-summary.md) and [BOM](BOM.csv). The [bottom-component list](redesign45A/placement/moved-to-bottom.csv) and [release holds](redesign45A/routed/changes-and-release-holds.md) are included.

The provisional four70um-copper stack, actual thermal performance, incoming/legacy termination ratings, M5 terminal stencil/hardware/support and special filled/capped via process require qualification. Balance connector paths remain intentionally open and unprotected; preserving the existing schematic does not implement balance-reversal protection. No manufacturing files are released.

The actual open source was C:/Users/sanga/Desktop/ReversePolarityProtection4MOSFET. Its77 files were backed up before modification; the untouched copy/manifest are in redesign45A/original-open-project-backup and original-open-project-sha256.json. The Desktop source is unchanged. Open this Documents/Codex project to see the routed version. Writing back to Desktop requires that folder to be in the writable workspace.

The earlier placement-only and60A studies remain historical snapshots on disk; the authoritative current material is redesign45A/routed. The routed ZIP includes native CAD, local libraries, BOM, current reports/images/calculations, approval record and source hash records; backup file folders remain on disk and are excluded from the ZIP. Optional KiCad stock3D models are not bundled. No actual Saturn results were obtained.
