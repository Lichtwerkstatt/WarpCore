# AGENDA

## Organizational
- [Download](https://www.freecadweb.org/) FreeCAD
- [Download](https://ultimaker.com/software/ultimaker-cura/) UltimakerCura 
- 2 Topic Workshop in One : Concepts, Ideas, Best Practices
- Questions / Discussions welcome
- Lichtwerkstatt, [Discord](https://discord.gg/kpjGXzdYek) : Open, Free, Mentoring
- Who knows CAD/3D Models /3D Printing?

## CAD
- Basic Workflow: IDEA -> 3D Model -> 3D Print
- History of technical Drawings:
  - Find Mistakes / Inconsistencies / Lack of Information
  - Smaller to Bigger Projects (matching parts)
  - Changes/Mistakes -> whole process of redrawing, communication, revision very expensive
- CAD as a solution: supervision/help
  - formal and clear unambigious model
  - model decisions (constraints), paramaters
  - limited set of operations
  - non-destructive Process(!), Computer calculates implications
- extended CAD today
  - CAD/CAM -> CAE
  - simulation
  - applications -> program interfaces, data im- and export
 
### CAD Programs
- Licences : FSU Autodesk Inventor, SolidWorks, PTC?
- Educational: [FUSION 360](https://www.autodesk.com/products/fusion-360/personal) (Maker), [OnShape](https://www.onshape.com/de/) (browserbased)
- Free to Use: FreeCAD, [TinkerCAD](https://www.tinkercad.com/), [OpenSCAD](https://openscad.org/)

### FreeCAD
- basic CAD program
- nice community, open development
- tutorials, easy to learn
- AddOns (Benches) , perfect for maker and hobby designer

#### PART Bench
- Start Page -> Benches
- PART Bench, Model / Properties
- Add Primitive, Properties, Transform, [Navigation](https://wiki.freecad.org/Mouse_navigation)
- Add Second Primitve for Bracket
- Boolean
- Change afterwards (Non Destructive)
- OPT: add Cylinder for Hole
  - Draft Array for both Bracket Sides

#### PART DESIGN
- Add Sketch for Box, Pad Sketch
- Skin
- Add Holes for PCB/Lid, Pad Holes
- Name, Constraints: Constraints.ScrewDiameter
- Spreadsheet, add Alias, access Alias Spreadsheet.ScrewDiameter

#### EXPORT
 - STL, Resolution
 - View in Editor
 - View in Blender

## 3D Printing
 - CAM method, compare to Lasercutting / CNC Milling
 - Methods [Overview](https://all3dp.com/2/3d-modeling-for-3d-printing-the-main-considerations/)
     - SLA (+ resins, layerheight) (-postprocessing, waste)
     - Sintering (+ metal, no support) (- expensive, powder everywhere)
     - FDM (+ cheap, easy to handle) (- materials)
 - Printers then and now
 - Filaments (PLA, PETG (ABS), TPU/PVA/... )

### Slicing
 - Setup and Import Model
 - Layer Height, Infill
 - Critical First Layer : Contact Surface, Adhesion Plate
 - Know your Printer :
    - Thermal Distortion, Holes, Dimensions
    - Overhangs, Bridging
    - Support Structures

### Best Practices
- [Design Rules](https://www.hydraresearch3d.com/design-rules)
- [Poster by Billie Rubens](https://blog.adafruit.com/2020/01/24/a-poster-of-cad-design-tips-for-3dprinting-cad-billierubenmake/)
- Overhangs 45° Rule -> Archs Tear Shaped
- Round Corners
- Chamfers on Bottom
- Support Inner Corners
- Orientation
- Cascading Bridges
- Complient Mechanisms
- Seperate Parts, Minimize Failure, FDM scales badly
- Example: OpenBikeSensor MainCase.stl
 
