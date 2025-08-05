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
  - \_ready Helloworld
    - Einführung Programmierung
    - Variablen
    - Zuweisung
    - Vergleich
    - Entscheidung
    - Objekte
  - \_process Test, position.y

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
- add script, draw with \_draw Function

```python
extends Control
func _draw() -> void:
	draw_circle(Vector2.ZERO, 3, Color.WHITE)
	draw_line(Vector2(0,-10),Vector2(0,-20),Color.WHITE,2)
```

## Adapt Jumping

- add variable for jump height instead of jump velocity
- umstellen Hmax = V^2 / 2g -> V = sqrt(Hmax\*2g)

```python
@export var jumpHeight : float = 1.0
...
velocity.y = sqrt(jumpHeight*2*get_gravity().length())
```

- add Test Level
  - add csgBox, move with Snapping (Shift Fine Movement)
  - Tweak Material, Albedo Orange
  - Duplicat and extend shapes in Snapping Mode (jumpable and unjumpable)

## Building a Sandbox Level

- new scene : first level
- save materials in material folder
  - add prototyping textures to materials
  - add albedo/texture
  - UV1 : triplanar, world triplanar
  - reset albedo color
- add csg box with prototyping material, flip faces
- use CSGcombiner node
- add larger structures with quickLoad Materials

## Adding a Weapon

- import GLB into new Weapons Folder, Double-Click -> Reimport
- Instatiate Child Scene, Transform Coordinates in Preview Mode
- New Scene Weapon
- Add Timer, name Cooldown
  - One Shot : True
- add Script to Weapon
  - add LMB as shoot

```python
var fire_rate := 14

@onready var cool_down = $CoolDown

func _process(delta):
	if Input.is_action_pressed("feuer") and cool_down.is_stopped():
		cool_down.start(1.0 / fire_rate)
		print("Weapon fired!")
```

- add inherited scene of weapon,
  - rename root node to SMG
  - save and name SMG
- copy weapon mesh from spieler to SMG scene
- add child scene SMG to spieler

### Adding Recoil and Raycasts

- define distance of recoil
- define weapon_mesh in weapon script to specify in SMG
- safe original position of weapon mesh in variable
- build shoot function with recoil
- lerp back in \_process

```python
@export var fire_rate := 14.0
@export var recoil := 0.05
@export var weapon_mesh : Node3D

@onready var cool_down = $CoolDown
@onready var weapon_position: Vector3 = weapon_mesh.position

func _process(delta):
	if Input.is_action_pressed("feuer") and cool_down.is_stopped():
		shoot()
	weapon_mesh.position =
		weapon_mesh.position.lerp(weapon_position, delta*10)

func shoot() -> void:
	cool_down.start(1.0 / fire_rate)
	print("Weapon fired!")
	weapon_mesh.position.z += recoil
```

- add Raycast3d to weapon scene
- change vector to 0,0,-100
- import onready in SMG script
- print(raycast.get_collider())

### Particles

- add GPUparticles node to SMG scene, align with barrel, rename MuzzleFlash
- Draw Passes, Mesh 1 : BoxMesh
- Process Material : Particle Process Material
- Resize Particle BoxMesh : 0.1m
- Time Explosiveness : 1
- Particle Process Material
  - Gravity : off
  - Initial Velocity : min 2, max 4 / min 6 to 10
  - Direction : 0 0 -1
  - Spread : 8
  - Display/Scale : new CurveTexture, right down
  - Lifetime : 1.0/14.0
  - Fixed FPS: 60
- Geometry Instance
  - Material Override, NewStandardMaterial3D
  - Emission : White, Energy 5
- Time: OneShot ON, Drawing Local Coords: ON, Shadows Cast Shadow OFF
- add export variable for muzzle_flash

```python
@export var muzzle_flash : GPUParticles3D
...
func shoot() -> void:
	muzzle_flash.restart()
```

- create new scene, gpuparticle node, rename sparks and save
- draw passes, pass 1 : new boxMesh, resize 0.1
- material override : emissive yellow material
- new ParticleProcessMaterial
  - spread 180
  - velocity : 1 to 5
  - display scale 0.5 to 1
  - scale curve like above
- Time Lifetime 0.5
- Explosiveness 1
- Cast Shadow Off
- Transform Top Level ON
- OneShot ON
- Add AnimationPlayer to SparkNode
  - new Animation named spark
    - Autoplay
    - Sparks Node -> Emitting Keyframe
    - first kreyframe : change value to on
  - add method track
    - last keyframe : queue_free() method
- weapon script
  - add export variable for packed scene
  - load sparks scene into inspector
  - instatiate and reposition sparks

```python
@export var sparks : PackedScene
...
var spark = sparks.instantiate()
add_child(spark)
spark.global_position = ray_cast_3d.get_collision_point()
```

## Ammunition (simple mode -> adapt later for multiple types of ammunition

- Add AmmoHandler node in Player Scene
- class_name AmmoHandler
- variable for Ammo amount
- get and set functions
  - has_ammo
  - use_ammo

```python
extends Node3D
class_name WeaponHandler

var ammo := 60

func has_ammo() -> bool:
	return(ammo > 0)

func use_ammo() -> void:
	ammo -= 1
	print("Munition : "+str(ammo))
```

- add ammo handler export variable to weapon script
- use_ammo in shoot function

```python
@export var weaponHandler : WeaponHandler
...
if weaponHandler.has_ammo() :
		weaponHandler.use_ammo()
		muzzle_flash.restart()
...
```

### Ammo Label

- add margin container in Player Scene, Full Screen, Apply Margin of 8
- add label bottom right
  - new LabelSettings
  - Fontsize up
- export label in AmmoHandler Script
- update label in \_ready and use_ammo

```python
@export var ammoLabel : Label
...
ammoLabel.text = str(ammo)
```

### Ammo Pickup

- new Scene based on Area3D name AmmoPickups
- add mesh cube, size 0.5 , angled
- add collision sphere 1m
- add script to root node
- add listener body_enters
- access export variable for weapon_handler in spieler script

```python
extends Area3D

@export var amount := 20

func _on_body_entered(body: Node3D) -> void:
	body.weapon_handler.add_ammo(amount)
	queue_free()
```

- update add_ammo function in weapon handler script

## Enemies

- set up **navigation server**
  - add navigation region to sandbox
  - new navmesh
  - put level under navmesh
  - bake mesh
- new scene, characterBody, rename **enemy**
- copy and paste mesh and collider from player scene
- add navigation agent
- attach script to root, template movement
  - comment move_and_slide
  - generate reference to nagivation agent
  - get reference to player by group
  - set player pos as target
- enable Debug Mode in Agent
- put player into new player group

### Enemy Movement

- delete unecessary code for movement
- add movement based on direction
- check for player in pickup script

```python
if body.is_in_group("player"):
		body.ammoHandler.add_ammo(amount)
		queue_free()
```

- adapt speed in enemy script

```python
@onready var navAgent = $NavigationAgent3D
var player

func _ready():
	player = get_tree().get_first_node_in_group("player")

func _physics_process(delta):
	navAgent.target_position = player.global_position
	var next_pos = navAgent.get_next_path_position()

	# Add the gravity.
	if not is_on_floor():
		velocity += get_gravity() * delta

	var direction = global_position.direction_to(next_pos)
	if direction:
		velocity.x = direction.x * SPEED
		velocity.z = direction.z * SPEED
	else:
		velocity.x = move_toward(velocity.x, 0, SPEED)
		velocity.z = move_toward(velocity.z, 0, SPEED)

	move_and_slide()
```

### Range Attack

- add provoked bool variable
- add export range value
- calculate distance
- set provoked based on distance
- only update next_pos when provoked

```python
  if aggro:
  navAgent.target_position = player.global_position
  var next_pos = navAgent.get_next_path_position()
  ...
  var distance = global_position.distance_to(player.global_position)
  if distance <= aggroRange:
  aggro = true
```

## Gimmicks

### Shootable Boxes

- new Scene Ballerkiste made of RigidObjects
- Mesh and Collider
- put in Group "impulse"
- extend shooting script by

```python
var object = ray_cast_3d.get_collider()
if object.is_in_group("impulse"):
	var from = ray_cast_3d.global_position
	var to = ray_cast_3d.get_collision_point()
	var impulse = (to-from).normalized() * 10
	object.apply_impulse(impulse,(object.global_position - to))
```
