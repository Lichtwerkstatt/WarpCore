# KiCAD PCB Design

**Date**: June, 1st, 2023  
**Time**: IMiP Lecture 12:00-16:00  
**Place**: ACP SR1

## Ressources

## Before start
- Arduino/ESP Workshop at [Hackathon](hacktheparadise.jena.de) June 17th.
  - Join, Learn and Play Around!
  - Build little Sensor Applications
  - Programming microcontrollers
  - sending Data (WiFi, LORA)
  - Soldering, Akku welding
- first time workshop
  - stay calm!
  - please give feedback
- [Download](https://www.kicad.org/download/) KiCAD 7.x


## Theory
- What do we want? Electrical Connection!
  - conducting, mechanical stress, heat resistant
- Mechanical connection
  - Screws & Clamps
  - Breadboards
  - Wires & Clippers (Banana Clips)
  - Wire Wrapping
  - Soldering on Strip Boards
  - Sculptures for [real](https://www.eurocircuits.com/wp-content/uploads/detektor-radio-1948-258px-high.jpg) and [art](https://www.google.com/search?q=circuit+sculpture)
- PCB (Printed Circuit Boards)
  - Substrate (Fibre Glas, Epoxy Resin) (Flame Resistant)
  - etched Copper Layer (top, bottom, multilayers)
  - Holes with electroplating
  - Solder Mask
  - Surface Finish (ENIG)
  - Silk Screen
- Let's talk about stuff:
  - PCB Design in the early days
  - PCB Design today for everyone!
  - PCB Art
  - Flex PCBs
- Famous PCBs
  - Paul Eisler PCBs
  - Raspberry Pi
  - Arduino

- Software
  - Designing all the layers based on Schematic
  - KiCAD is a Software Suite:
    - Create Symbols for Components
    - Design Schematic
    - Create Footprints for Components
    - Generate netlist
    - Board Layout
    - Production
    - Generate BOM
  - KiCAD is not (particularly) for
    - Circuit Simulation
    - Heat and E/M field distribution
    - Fitting tests
- Startup KiCAD
  - Generate New Project / Folder
  - Get familiar with User Interface
    - Component and Footprint Libraries
    - Help

## Step 1 Schematic Design
- Open EESchema
- Configure Page Layout
  - Title
  - Rev
  - Date
  - Name
  - Licence etc.
- Scroll / Press Scroll for Zooming and Paning
- Add Component (A)
- Rotate (R), Move (M), Pull (G)
- Flags (GND, PWR)
- Wires (W)

### Build Blinking Light (LED Flasher)
- [Flashing LED](https://www.elprocus.com/wp-content/uploads/Blinking-LED-using-555-timer.jpg) based on 555 Timer
- Add Component NE555D
- Add three resistors, polarized condensators and a LED
- Add Voltage Source
- add VCC and GND flags
- wire everything up

### Step Add Component Symbol


### Special Step Simulations in KiCAD with Spice
**555 Timer Simulation**
![555 Flasher Schematic](files/555flasher_schematic.JPG)
- add Spice Model to 555 Timer
- add Spice Model to Diode (QLP...)
- have values for every component
- have an id for every component
- add output flag
- .tran 1u 20m 2m uic directive

**Capacitor Load Cycle**
- add voltage supply (spice / VDC)
- add resistor and capacitor
- add reference point (0)
- VDC 15V, 100kOhm, 10uF
- .tran 0.1 10 uic directive


**Exercise** : Draw a schematic for a Laser Diode Driver (Constant Current Source) in KiCAD.

## Step 2 Assign Footprints

### Step Design your own Footprint

## Step 3 PCB Design

## Step 4 Generate Gerber Files and BOM

 