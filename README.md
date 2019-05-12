# Teardrops

This action plugin adds and deletes teardrops to a PCB.<br>
Based on https://github.com/svofski/kicad-teardrops.<br>
This implementation uses zones instead of arcs. This allows to comply with DRC rules by simply rebuild all zones. You can also modify their shape by simply modifying the zone outline (like any other zone).
Teardrops created with this script use a specific priority (0x4242) to be recognized as teardrops.

![Teardrop dialog](rcs/screenshot.png?raw=true "Teardrop menu")

## Install
Just copy the teardop folder into the ~/.kicad_plugins directory, then restart Kicad. The teardrop plugin should now be available in the Tools/External plugin menu.

## Add Teardrops
Select some vias/pads on which you want to add teardrops. Or don't select anything to apply teardrops on all vias/pads<br>
Three parameters are available: hpercent, vpercent, segs.<br>
Segs defines the number of segments in one teardrop curve (default = 10). Setting segs=2 will disable curved teardrops and use straight lines instead.<br>
Vpercent (default 70%) and hpercent (default 30%) define the teardrop dimensions (relative to via/pad size) according to the Altium way (for via only):
http://techdocs.altium.com/sites/default/files/wiki_attachments/235632/TeardropsDlg.png<br>
When curved teardrops are selected (segs>2), the vpercent maximum is 70%.

## Remove all teardrops
This will remove all the teardrops from the PCB.<br>
If you want to suppress a single teardrop, don't use this menu. Just delete the coresponding zone by hand.

## Note 1:
In order for a zone to be recognized as teardrop by the script, the zone must meet the 2 following requirements:
- the via/pad center must be contained within the zone
- the center of the zone's bounding box must be located within the track

## Note 2:
It is still possible to use the old form of this script (non action plugin). The td.py script remains fully functional for independant use.

## Note 3:
Newly inserted vias are not visible immediadly due to a bug in Kicad/pcbnew refresh system. The following sequence is recommended after teardrop insertion:
1. Save the pcb design
2. Quit pcbnew
3. Reopen the design in pcbnew
