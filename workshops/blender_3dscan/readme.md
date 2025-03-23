# Blender Introduction and 3D Scan Postprocessing

Datenwerkstatt 24.3.2025
Deutsch

## Ressources

- Optimize Scans in Blender [YouTube](https://www.youtube.com/watch?v=I-lH2_Ca3Dw&ab_channel=MicroSingularity)
- Tutorial Fix Holes Potogrammetry [YouTube](https://www.youtube.com/watch?v=_pzTK-LBm3o&t=2081s&ab_channel=BlenderBones)
- Tutorial Optimise Photogrammetry Scans [YouTube](https://www.youtube.com/watch?v=I-lH2_Ca3Dw&ab_channel=MicroSingularity)
- Tutorial Homemade Bread Retopo [YouTube](https://www.youtube.com/watch?v=Yx9TvvnxCAM&ab_channel=Markom3D)
- 3D Scan Homemade Bread [Sketchfab](https://sketchfab.com/3d-models/homemade-bread-rawscan-f95a2e18d8454902a779360306d680c5#download)
- Retopology Software [GitHub](https://github.com/wjakob/instant-meshes?tab=readme-ov-file)

## Workshop Files

- Bread Raw Scan + Textures
- HDRI

## Intro

- Lichtwerkstatt
- Ausstattung
- Workshop-Programm
- Blender Einsatz
  - 3D Druck
  - 3D Scan
  - Poster
  - Publikationen
  - GameDesign

## Einstieg in Blender

Intro:

- Blender 3D Suite / Generalist Software
- Addons (Import, Funktionen)
  - Microscopy Nodes
  - BlenderGIS
  - Blender Molecular Nodes
  - Bioxel
  - Blender for Biologists
- Animation/Bilder : 2D/3D/StopMotion

GUI

- Panels
- Viewport

Transform

Object/Mesh

- Edit
- AutoSmooth

Material

- Shader nodes
- UV Mapping

Sculpting

## 3D Scans

### Methods

Quellen:

- Sketchfab
- MyMiniFactory (World Heritage)

### Data

3D Files

- CAD
- Mesh : STL
- 3D Objects: OBJ, GlTF, FBX
- Point Cloudes

### Check out

- Statistics
- Show Wireframe
- Holes (Face Orientation)

Textures:

- Einführung UV Mapping
- Textures
- Occlusion / Normal

Rendering:

- Animation Rotation
- Rendering / Lights
  - HDRI

## Repair Meshes

- Select Outlier
- Fill Holes
- Merge by Distance
- Sculpting

## Retopology

- Idea

  - Loss of Information
  - Further Processing / Visualization

- Duplicate Object and hide Original
- Turn off Auto Smooth
- Variante 1)
  - Decimate Modifier
  - Problem -> Quad Mesh
- Problem Texture!

## Bake Texture

- Variante 2)
  Remesh -> Voxel Remesh
- Variante 3)
  Remesh Modifier, Fills Holes
- InstantMeshes Programm
- Redefine UVs

## Bake Normals

- Add Modifier Multires
- Add Modifier Shrinkwrap,
  - Method Project
  - Target Original Pane
  - Negative and Positive
- Subdivide 3times in Multires
- Apply Shrinkwrap
- Multires Levels Viewport 0
- Add Image Texture & Normal Map Node
  - Generate new Diffuse Map 2K, no Alpha, 32bit

## Backside Culling

- Innenräume (Bsp Münchner Institut)
- BSDF -> Mix Shader -> Output
- Geometry/Backside -> Fac
- Transparent BSDF -> Shader 2

## Point Cloud

- LiDAR Data
  - no Mesh Reconstruction
  - ne Texture (only Color per Point)
  - Schnell und easy, sehr genau
- Import PLY
- Now Programming?!
- Geometry Nodes Workspace
- Mesh to Points (play with radius)
- Add new Shader, Combine Color aus
  - Attribute mit diffuse_red,...
  - Fac -> Divide by 255
  - Into Combine Color
- GN : add Set Material
- Set up Light

Alternativ

- GN
  - Input zu Points to Volume
  - zu Volume to Mesh
  - zu Output

## Mehr Komplexität

- Bsp Pilz
