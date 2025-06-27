# Godot for Kids

June, 2025

## Intro

## Setup Project

## First Test

- Node2D Tree Structure
- Insert Label, Rename -> Inspector
- Insert Sprite Godot Logo (Inspector)
- Adding Script, \_start and \_process, print()
- Movement

```python
var speed := 200
var rotation_speed := 3

func _ready():
	pass # Replace with function body.

func _process(delta):
	var direction := Vector2.ZERO

	# Bewegung (Pfeiltasten oder WASD)
	if Input.is_action_pressed("ui_up"):
		direction.y -= 1
...

	position += direction * delta * speed

	# Rotation mit Q und E
	if Input.is_key_pressed(KEY_Q):
		rotation -= rotation_speed * delta
...

```

- Movement along up-Vector

```python
if Input.is_action_pressed("ui_left"):
        rotation -= rotation_speed * delta
    if Input.is_action_pressed("ui_right"):
        rotation += rotation_speed * delta

    var velocity := Vector2.ZERO

    if Input.is_action_pressed("ui_up"):
        velocity = -transform.y * speed
    elif Input.is_action_pressed("ui_down"):
        velocity = transform.y * speed

    position += velocity * delta
```
