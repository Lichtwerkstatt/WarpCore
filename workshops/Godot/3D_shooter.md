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

