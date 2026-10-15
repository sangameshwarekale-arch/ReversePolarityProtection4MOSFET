# Routed engineering evaluation, revision E

The approved placement has been routed in the native KiCad9 project. Open the main .kicad_pro in the project root. The Desktop original remains untouched; this editable version is saved under Documents/Codex.

- [Original/front/rear comparison](images/routed-comparison.png)
- [Native front](images/front.png), [mirrored rear](images/rear.png), [inner1](images/inner1.png), [inner2](images/inner2.png), [schematic](images/schematic.png)
- [Final check summary](reports/check-summary.md) and [native audit](reports/final-preservation-and-connectivity.json)
- [Routing, electrical and thermal calculations](calculations/routing-calculations.md)
- [Changes and release holds](changes-and-release-holds.md)
- [18 components moved to bottom](../placement/moved-to-bottom.csv)

ERC0; DRC0 errors/12 original missing-courtyard warnings;0 unconnected;0 parity issues. These checks do not qualify45A operation. Balance protection remains unimplemented, incoming/legacy terminations are unrated, thermal/process/mechanical conditions remain unresolved, and one via requires filling/capping. Manufacturing outputs are withheld.
