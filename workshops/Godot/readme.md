# Godot for Kids

June, 2025

## Intro

- Introduction
- Lichtwerkstatt
- Relation to Game Dev
- Ask
  - Age
  - Background
  - Preknowledge Programming
  - Projects?
  - English?
- LW Workshop Gaming&Creatvity
- Game Engines, What for?
- Tasks for Game Engine
- Common Game Engines
- Game Tree

## Setup Project

- New Project

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

- add StaticBody2D under Sprite (Warning Sign)
- add CollisionShape2D, Define Shape, Resize Shape

### Character and Moving

- Download [Assets](https://pixelfrog-assets.itch.io/treasure-hunters) from https://pixelfrog-assets.itch.io/treasure-hunters
- add CharacterBody2D, with CollisionShape (Pill)
- add Sprite TH>CaptainClownNose>Sprites>CptClownNose>withoutSword>Idle>idle01.png
- adjust bluriness : Project Settings/Renderin/Textures/Default Filter : Linear to Nearest
- adjust position to axis of CharacterBody, Collision Shaper over Pixel Art
- Save Branch as New Scene -> own Object
- add Character2D Script

```python
extends CharacterBody2D


const SPEED = 300.0
const JUMP_VELOCITY = -400.0

# Get the gravity from the project settings to be synced with RigidBody nodes.
var gravity = ProjectSettings.get_setting("physics/2d/default_gravity")


func _physics_process(delta):
	# Add the gravity.
	if not is_on_floor():
		velocity.y += gravity * delta

	# Handle jump.
	if Input.is_action_just_pressed("ui_accept") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	# Get the input direction and handle the movement/deceleration.
	# As good practice, you should replace UI actions with custom gameplay actions.
	var direction = Input.get_axis("ui_left", "ui_right")
	if direction:
		velocity.x = direction * SPEED
	else:
		velocity.x = move_toward(velocity.x, 0, SPEED)

	move_and_slide()
```

### Character Looking

- open Character, Look int Sprite / Offset / FlipH
- Character Script

```python
@onready var _sprite : Sprite2D = $Sprite2D

func guck_links():
	_sprite.flip_h = true
	pass

func guck_rechts():
	_sprite.flip_h = false
	pass

...

if sign(direction) == -1:
	guck_links()
elif sign(direction) == 1:
	guck_rechts()
```

### Camera

- add camera to main scene
- scale down
- put under character

### Animation

- add AnimationPlayer to Sprite
- add Animation named "idle"
- add Track, Property, Sprite, Texture
- insert key with RMB, every 0.1s, populate with idle textures
- reduce length to 0.5s
- loop animation
- repeat for run and jump
- put animationTree under AnimationPlayer
  - assign animationplayer to Anim Player Property
  - Tree Root : NewAnimationPlayerStateMachine
  - add Animations (idle, run,...)
  - start -> idle
  - idle -> run (Advanced / Expression : velocity.x != 0)
    - advanced expression base node : Root Note
  - run -> idle (velocity.x == 0)
  - run -> jump (velocity.y < 0)
  - jump -> idle (velocity.y == 0)

### World Building

- Add Tilemap to Scene
- Define Tileset, Change Tilesize to 32x32
- Add Physical Layer (for later Collision)
- Add Terrain -> name Island
- Goto Tilesets and Import Graphics
  - TH/Palm Island/Sprites/Terrain/Terrain32x32
- Goto Tilemap
  - drawing, erasing
- Add Physics Collision
  - goto Tileset
  - Select, All
  - Physics, Layer 0
  - Click ... , Reset to Default Tile Size
  - Physics, Polygon, Einweg -> Jump Through

### Locomotion Effects

- Add AnimatedSprite2D to Character Scene "Dust Particles"
- Add Sprite Frames
- Add CptClownNose/Sprites/DustParticles/JUMP
- use Offset to Align under Character
- Change Framerate to 10/s
- save as new Scene
- add Script
- func \_ready(): play()
- Signals : animation_finished, Connect to Method
  queue_free()
- copy scene for different particle effects
- Character Script :

```python
@export var _jump_dust:PackedScene //assign in inspector

func _spawn_dust(dust):
    var _dust = dust.instantiate()
    _dust.position = position
    get_parent().add_child(_dust)

_spawn_dust(_jump_dust)
```

### Treasures

- Start with a global Data Script
- Project Settings, Globals

```python
extends Node

@export var points : int
@export var lives : int

signal points_changed

func _init():
	points = 0
	lives = 3

func incPoints(value):
	points += value
	emit_signal("points_changed", points)
```

- add Node2D Treasures, Area2D, Animated Sprite
- TH/Treasures/Sprites/Silvercoin, 10FPS, Loop, Autoplay
- add second animation effect, coin effect no loop
- add Collisionshape2D
- make Coin into Scene
- adding script :

```python
extends Area2D

@onready var _sprite : AnimatedSprite2D = $AnimatedSprite2D

func _on_body_entered(body : Node):
	if not body is CharacterBody2D:
		return
	Global.incPoints(1)
	_sprite.play("effect")
	await _sprite.animation_finished
	queue_free()


```

- duplicate to gold coin, new Animation
- export value and adjust in inspector

### UI

- CanvasLayer
- Add TextureRec with Coin as Icon
- Label behinde
- Add Script:

```python
extends Label

# Called when the node enters the scene tree for the first time.
func _ready():
	Global.connect("points_changed", Callable(self, "_on_points_changed"))

# Called every frame. 'delta' is the elapsed time since the previous frame.
func _on_points_changed(value):
	self.text = "Coins: %d" % value  # "Coins: 10"
	pass

```
