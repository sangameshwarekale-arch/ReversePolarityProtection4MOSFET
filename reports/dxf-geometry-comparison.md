# Supplied DXF geometry inspection

Source: `C:\Users\sanga\Downloads\battery-pcb (3).dxf`; SHA256 `d188c32c0ad89ea83bbbaa86f76326fb693a87f1fa55b4efa4f02ee1dd4463d8`. Read only.

- DXF unit declaration: millimetres (INSUNITS=4).
- Outline centreline bounding dimensions: 44.520 x 41.506 mm. Displayed polyline stroke is0.254mm; its enlarged drawing bounds are not a change to the outline centreline.
- All24 drilled-pad centres match the existing KiCad mechanical pad locations after origin translation /Y-axis inversion. Maximum discrepancy: 0.000001mm (DXF export rounding).
- The drawing shows15 header-contact holes along a2.5mm pitch row, seven curved cell-tap holes and two larger wire-termination holes. It includes G/B1-B6 labels and top/bottom trace geometry.
- These geometric traces/labels do not establish connector current ratings, copper thickness, netlist correctness, BMS pin limits, balancing current or misconnection behavior. They do not demonstrate that raw balance paths can remain connected safely during main-lead reversal.
- The four-device starter retains the original mechanical geometry and deliberately omits raw balance copper pass-through pending interface protection design. Components are unplaced; physical fitting/routing and thermal copper are not validated.
