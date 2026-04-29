---
layout: default
title: "Coop Dungeon p2"
---
# Coop Dungeon p2

difference between .new and .instantate:
We used .new for ENetMultiplayerPeer.new,
as it is also a instancing it why do we use .instantiate for scenes that we ourselves created? Because EnedMultiplayerPeer is a class?

## **The Core Difference**

**`.new()`** = Creates an instance of a **class** from code
**`.instantiate()`** = Creates an instance of a **PackedScene** (a saved scene file)

EnetMultiplayerPeer is a built-in Godot class, it is code, not a scene file. When using .new, we tell godot to allocate memory for the EnetMultiplayerPeer object and call its "init()" constructor.

EnetMultiplayerPeer is a class defined in c++ that inherits from MultiplayerPeer.

When using .instantiate for packed scenes, its not a class definition but a serialized copy of a scene file saved to disk. It is a data structure containing scene tree information like nodes and properties.

When using .instantiate we tell godot to deserialize that scene file, create all nodes within, restore the properties and give me the root node of the unpacked tree. It is a reconstruction operation, not just the creation of an empty object.

Both have different return types, .new returns an instance of the class, .instantiate the root node of the unpacked scene.

<mark>Both are "Instantations" conceptually, hence why they could be mixed up. Even though in the end an object gets created in memory, these are different kind of instantiations.</mark>

# lambda function / anonymous function
The reason why it is called lambda because in computer programming lambda means anonymous function, as in the mathematical terms lamdba means unnamed function.

So this is the same as a normal written out function. Following are two comparisons:

Normal
```gdscript
multiplayer_spawner.spawn_function = func(data):
	print(data)
	return 42
```

Lambda
```gdscript
func spawn_player(data):
	print(data)
	return 42

multiplayer_spawner.spawn_function = spawn_player
```

Or in the classic hello world example:

Normal
```gdscript
func _ready():
	var my_function = hello_world
	my_function()

func hello_world():
	print("hello world")
```

Lambda
```gdscript
func _ready():
	var my_function = func():      # ← CREATE the function here
		print("hello world")
	
	my_function()                   # ← CALL the function stored in my_function
```
The interesting thing about the lambda hello world example is, that the function can only be called inside of the ready function. Once ready finishes it no longer exists.


So what does the MultiplayerSpawner Node do?
When the authority (in this case the server) gets connections from his peers, it needs to replicate all nodes on all connected peers. When clicking on remote when the game is running you can see the different root nodes of all clients and the servers, all with their respective id. This one has to be unique per client, otherwise they differ between peers.

Credit: Firebelley Games (Coop Tutorial, check it out!)
