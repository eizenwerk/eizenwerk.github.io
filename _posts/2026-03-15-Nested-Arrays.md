---
layout: default
title: "Nested Arrays"
---

# Nested Arrays

Fuck man, what a chad!

![](/assets/blog/2026-03-15-Nested-Arrays/Pasted image 20260315155351.png)
(cakez77 on twitch)

I need to continue pumping more. The last couple of days I didnt do as much as I wanted, I had too much personal stuff going on. BUT, i did a little bit every day. I was tired, fucking sleepy, exhausted, but I pushed through - and I am fucking proud of that. I always struggled hard with being consistent. This is my biggest flaw, and I want to tackle that. Using something that interest and motivates me and fills my internal need to create something, and it behaves like a jumpstart.

So what are we doing today? In the last couple of days the creation of dungeons was my focus, and the biggest issue I had was not being able to create an array inside an array without external help. I need to tackle that. Being creative seems easy to me, the level prototype also took some days, but it didnt feel difficult. Creating code does, and I **want** to create code. I always was envious of people who could. And I have time, why not use my time for something worthwile, instead of wasting my time on youtube and memesites.

Lets tackle creating arrays inside of arrays again. I may need some training.

A nested array is just an array inside an array. Visually it would look like this:
```gdscript
[1][2][3]            dungeon[0] = [1][2][3]
[4][5][6]     -->    dungeon[1] = [4][5][6]
[7][8][9]            dungeon[2] = [7][8][9]
```
`to access 5 you would use dungeon[1][1] (row 1, column 1)`

Lets focus on what I am trying to achieve.

I want to create a grid based on the size of the map. In the future, lower levels have bigger sizes. I am not sure if that is a good decision yet, as I do not know if the player brain likes that. Testing is needed. As the difficulty also scales, this could be a bad decision. At the same time, more enemies mean more loot. Maybe people want that when they invest time to get to specific lower levels for specific loot. Enemy spawns are limited by the dungeon level. 0-5 easy enemies like slimes, they spawn slime stuff, 6-10 are goblins, they spawn goblin stuff. As one needs to sell stuff they find in the dungeons, the economy is scaled around this. More work -> more scarcity > more expensive items. This is the current approach. If I have the base system running I can change some mechanics, the most important thing right now is to get nested arrays and some code running.

So what are the next steps? What does my dungeon generator need to do? Define targets and break down the underlying mechanics. Start from the end.

Target: Finished Dungeon, with a spawn room, a Boss room, some chest rooms, connection between these rooms which are all valid. Try to minimize cycles. I need variations in the connections (no straight lines), no repeating unreal paths.

- Reference the max size of the grid limited by the map size.
- Create a 2d grid and fill it with positional values
- Loop through the array and insert rooms (1x bossroom, 1x spawn, 2x chest room, multiple empty rooms with different sizes) ! Chest rooms need to have defined sizes. People need to associate the good feeling of loot with the environment, that way they "hunt" for these sizes.
- Check for overlapping, if it overlaps, recreate the room somewhere else until it does not
-...

So there are a lot of dungeon algos and I thought about what feels bad for players and what could fit the game mechanic. And even if I want to create a recettear inspired game, I want to put my spin on it. So the question is not, what do people like or not like, the question is, what do I want to feel in a dungeon?

I dont want to go in there hunting for a location which is marked or something like that
I want to be distracted by the dungeon itself, constantly in flow state
I want to be challenged, I want to have fun, I want to win
And in the end, I want a big sack of loot as a reward for my challenge.

Recommended algo for my approach:
Constrained room placement + tree spine

So what does that mean?
Create rooms

initial code for array generation and filling
```gdscript
extends Node3D

var array = []
var mapsize = Vector2(32,32)
var counter = 0

# Called when the node enters the scene tree for the first time.
func _ready() -> void:
	fill_array()
	print_array()


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta: float) -> void:
	pass

func fill_array():
	for y in mapsize.y:
		array.append([])
		for x in mapsize.x:
			array[y].append(counter)
			counter += 1

func print_array():
	for i in mapsize.y:
		print(array[i])

```

Wow I did a lot today and learned a lot. There was no time for noting a lot of things down, but I had to sketch some things down im my notebook.

This is the current code, i still have out of bounds issues and the path doesnt look like how i want it yet.

```gdscript
extends Node3D

var array = []
var mapsize = Vector2(12,12)
var s = 0

# Called when the node enters the scene tree for the first time.
func _ready() -> void:
	fill_array()
	generate_path()
	print_array()


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta: float) -> void:
	pass

func generate_path():
	var start_positionY
	var start_positionX
	# create starting position
	start_positionY = randi_range(0,mapsize.y-1)
	start_positionX = randi_range(0,mapsize.x-1)
	array[start_positionY][start_positionX] = 1
	#TODO add border buffer zone
	print("array start position")
	print(start_positionY,start_positionX)

	#for x in min_distance:
		#select random direction
		#check if potential position has a anything else than 0
		#insert something if no
		#select random direction if yes
		#repeat
	
	var min_distance = 20
	var current_positionY = start_positionY
	var current_positionX = start_positionX
			
	for x in min_distance:
		var direction = randi_range(1,4)
		match direction:
			1:
				print("UP")
				current_positionY -= 1
			2:
				print("RIGHT")
				current_positionX += 1
			3:
				print("DOWN")
				current_positionY += 1
			4:
				print("LEFT")
				current_positionX -= 1
		
		#check for out of bounds
		if current_positionX < mapsize.x and current_positionY < mapsize.y:
			#validating next cell
			if array[current_positionY][current_positionX] == 1:
				continue
			
			# validating perpendicular 
			if direction == 1 or direction == 3:
				if current_positionX < mapsize.x and current_positionX -1 >= 0:
					if array[current_positionY][current_positionX + 1] == 2 or array[current_positionY][current_positionX - 1] == 2:
						continue
			if direction == 2 or direction == 4:
				if current_positionY + 1 < mapsize.y and current_positionY -1 >= 0:
					if array[current_positionY + 1][current_positionX] == 2 or array[current_positionY - 1][current_positionX] == 2:
						continue
		else:
			continue
		
		array[current_positionY][current_positionX] = 2
		print(current_positionY, current_positionX)
		
func fill_array():
	for y in mapsize.y:
		array.append([])
		for x in mapsize.x:
			array[y].append(0)

func print_array():
	for i in mapsize.y:
		print(array[i])
		

```

Maybe I do not need prefab rooms? I set up the walls and doors in a modular way. Rooms could have a min size and they themselves could have walls in them. A real random "procedural" approach?

![](/assets/blog/2026-03-15-Nested-Arrays/Pasted image 20260315200429.png)

Also, I want this game to be deterministic. Dungeons should have hashes. If one wants to replay dungeons, one could use the replay function and paste the has from the play history into the replay function, setup his equipment and retry the dungeon if he wants. This is good for players who aim for skill.














Code:
```gdscript
extends Node3D

var array = []
var mapsize = Vector2(3,4)
var counter = 0

# Called when the node enters the scene tree for the first time.
func _ready() -> void:
	fill_array()
	print_array()


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta: float) -> void:
	pass

func fill_array():
	for y in mapsize.y:
		array.append([])
		for x in mapsize.x:
			array[y].append(counter)
			counter += 1

func print_array():
	for i in mapsize.y:
		print(array[i])

```

Output:

![](/assets/blog/2026-03-15-Nested-Arrays/Pasted image 20260313235625.png)




# related 

I think I found this on steam?

![](/assets/blog/2026-03-15-Nested-Arrays/Pasted image 20260426201520.png)


