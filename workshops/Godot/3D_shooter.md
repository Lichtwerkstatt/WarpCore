# 3D Shooter
Ferienworkshop 4.-8.8.2025

## Prep
- Frage Programmierung
- Frage Mathematik
- Frage Englisch

## Setup Project
- New Project (Forward+)
- Sprache auf DE stellen
- new 3D Scene
  - rename to Sandbox 
  - Save Scene as Sandbox
- Add CSBox3D (64x64x1m)
  - move 0.5m down (groundfloor)
  - enable UseCollision
  - rename to floor
- Sun/Environment
  - add Sun and Environment
  - rename Elements
- add Camera
  - rename
  - move slightly up
 
## Interlude
- Add RigidBody3D
  - Add MeshInstance3D
  - Add CollisionShape3D
  - move RigidBody up, rotate slightly
  - Run Game
- Add Script to RigidBody (Default Template)
  - _ready Helloworld
  	- Einführung Programmierung
    - Variablen
    - Zuweisung
    - Vergleich
    - Entscheidung
    - Objekte	
  - _process Test, position.y
```python
if Input.is_action_pressed("ui_right"):
	position.x = position.x + 0.1
if Input.is_action_pressed("ui_left"):
	position.x = position.x - 1 * delta
if Input.is_action_pressed("ui_up"):
	position.y += delta
```
**TODO** Umbauen auf Velocity Vector
Introduction into Vectormath
   
## 1st Person Movement
- Create New Scene, Root : CharacterBody3D
	- rename Player
	- add MeshInstance3D:Capsule
 	- add CollisionShape3D:Capsule
- Attach Script : Templaste CharacterBody3D
	- Explain Code
- ? New Input Bindings "move_forward", "move_left", ... and "jump"
- SandbooxRootNode RMB -> Instantiate Child Scene : Player
 	- move 1m up
- Move Campera to Player

## Looking around
### Horizontally
```python
func _input(event:InputEvent) -> void:
	print(event)
```
```python
func _ready()->void:
	Input.mouse_mode = Input.MOUSE_MODE_CAPTURED
...
func _input(event:InputEvent) -> void:
	if event is InputEventMouseMotion:
		rotate_y(-event.relative.x * 0.001)
	if event.is_action_pressed("ui_cancel"):
		Input.mouse_mode = Input.MOUSE_MODE_VISIBLE
```
### Vertically
- add camera to Player, move up 0.3m
- cerate @onready variable by Ctrl-Dragging into script
```python
camera_3d.rotate_x(-event.relative.y*0.001)
camera_3d.rotation_degrees.x = clampf(
	camera_3d.rotation_degrees.x, -90.0, 90.0)
```
- Clamp value to prevent overshoot
- optional : smoothing

### Reticles
- Player Scene Root, add Center Container
- Size Options -> FUll Screen
- Add ControlNode, rename to Crosshair
- add script, draw with _draw Function
```python
extends Control
func _draw() -> void:
	draw_circle(Vector2.ZERO, 3, Color.WHITE)
	draw_line(Vector2(0,-10),Vector2(0,-20),Color.WHITE,2)
```
## Adapt Jumping
- add variable for jump height instead of jump velocity
- umstellen Hmax = V^2 / 2g -> V = sqrt(Hmax*2g)
```python
@export var jumpHeight : float = 1.0
...
velocity.y = sqrt(jumpHeight*2*get_gravity().length())
```
- add Test Level
  - add csgBox, move with Snapping (Shift Fine Movement)
  - Tweak Material, Albedo Orange
  - Duplicat and extend shapes in Snapping Mode (jumpable and unjumpable)











