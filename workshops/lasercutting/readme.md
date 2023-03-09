# Introduction into Lasercutting

**Date** : March, 9th 2023  
**Time** : 5pm - 8pm  
**Place** : ACP SR2

# Prepwork
- Demo Material
  - Showcase Objects
  - Laptop Stand
  - Kerf Cuts
- Software
  - Inkscape [Homepage](https://inkscape.org)
  - FreeCAD [Homepage](https://www.freecad.org)
  - Fusion 360 [Homepage](https://www.autodesk.de/products/fusion-360)
  - Slicer for Fusion360 [Download](/https://knowledge.autodesk.com/de/support/fusion-360/downloads/caas/downloads/downloads/DEU/content/slicer-for-fusion-360.html)

# Agenda

## Welcome
- The Lichtwerkstatt
- Projekts / Devices / Workshops
- Modus Operandi
  - Question everything and immediatly
  - Bring in your own projects
  - Google! YouTube!

## Theory
 - Concept of Cutting and Engraving
 - Lasers
   - Laser Medium
   - Electron Energy Levels
   - Chain Reaction and Pumping
   - Resonator
   - Result:
     - high energy density
     - low divergence
     - phase synchrone, polarized

## Lasercutter
  - Laser Tube
  - Mirrors
  - Head
  - Stepper Motors
  - Control Unit
  - Laser Bed (Honeycomb Pattern)
  - Gas Supply (Air, Nitrogen)
  - Exhaust System

## Application
  - VECTORING / Cutting
    - vector path
    - constant pulsed beam
    - speed / power
    - focus (kerf distribution top/bottom)
  - RASTERING / Engraving
    - line by line (depends on resolution)
    - modulate power according to greyscale image -> engrave depth
  
## Materials
  - Do NOT lase when unsure!
  - Google!
  - YES
    - Acrylics PMMA, PE, PS, PET, PETG, ABS, ...
    - Wood, Plywood, MDF, HDF
    - Paper, Cardboard
    - (Stamp) Rubber
    - anodized, painted metal
  - **NO!!!**
    - Vinyl PVC
    - Anything with Halogens (Chlor, Brom, Jod, Fluor,...)
    - Carbon, PCBs
    - Neopren
    - Artificial Leather
    - Metal
  - Parameters
    - Look at [Manual](https://www.epiloglaser.com/assets/downloads/manuals/legend-manual-web.pdf)
    - Look at List in Lichtwerkstatt Lab
    - Google! Most Fablabs, Makerspaces provide a Wiki with extensive Lists. [example](https://wiki.happylab.at/w/Laser_Cutter#Materialien)

# Operation

## Prepare Files for Lasercutting
  - We need Vector Paths for Cutting
  -> Vector Tutorial
  - Add Kerf if desired (laser width 0,5mm)
  - Using Epilog Print Driver
    - save / export as PDF
    - Size Material, Laser Bed (610 x 457 mm)
    - Cut Pfade Kontur < 0.02mm
  - Using VisiCut [Documentation](https://visicut.org/)
    - use seperate Layers for Cutting / Engraving
    - Filter by Layers

## Lasercutting Operation
  1. Switch Laser on 
  1. Put in material
  1. Adjust Focus if desired
     - move Bed up/down Button
     - move Bed with Arrows
     - Reset Button
  1. Reset HomePosition
     - use target laser if desired
     - disable X/Y Button
     - confirm with green
     - move laser head to desired position
     - reset Home Button
  1. Switch on Gas Supply
     - if nitrogren LED is on everything is fine
     - else press and hold Gas Select for 5sec
     - press nitrogen on/off when green light is up 
     - if nothing happens switch on air condition first
     - make sure, that nitrogen supply is turned on and at 2bar at gas valve
  1. send data from program to lasercutter
     - file and job number should appear on display
  1. switch on exhaust system
  1. press GO Button!
  



# Ressources

## Tutorials
- Using [FreeCAD](https://www.youtube.com/watch?v=ikip-g5qPhA&ab_channel=WayofWood) with Lasercutting Workbench (YouTube)
- Design for Lasercutting in [Fusion 360](ttps://www.youtube.com/watch?v=7riGolu7BpA) (YouTube)
- Design in Fusion 360 with [DXF Lasercutting Plugin](https://www.youtube.com/watch?v=0deCkiEjdTk) (YouTube)

## Tools and Sources
- Models and Projects on [Thingiverse](https://www.thingiverse.com/search?q=lasercut)
- [Boxes.py](https://www.festi.info/boxes.py/) Box Design Generator
- [Collection](https://cleversomeday.com/svgtools/) of Generators for Cutting
- Another [Collection](https://makerdesignlab.com/tutorials-tips/online-file-generators-for-laser-cutting/) of Generators for Mazes, Gears, etc.

## Programs and Plugins
- Autodesk [123Make](https://autodesk-123d-make.en.softonic.com/)
- [Slicer](https://knowledge.autodesk.com/de/support/fusion-360/downloads/caas/downloads/downloads/DEU/content/slicer-for-fusion-360.html) for Fusion
- [Pepakura](https://www.instructables.com/Papercraft-With-Blender/) Plugin for [Blender](https://www.blender.org/)
