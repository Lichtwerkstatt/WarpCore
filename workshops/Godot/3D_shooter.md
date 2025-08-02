# 3D Shooter
Ferienworkshop 4.-8.8.2025

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
  - _ready Helloworld, Berechnung
  - _process Test, position.y
```python
if Input.is_action_pressed("ui_right"):
		position.x = position.x + 0.1
	if Input.is_action_pressed("ui_left"):
		position.x = position.x - 1 * delta
	if Input.is_action_pressed("ui_up"):
		position.y += delta
```
   
