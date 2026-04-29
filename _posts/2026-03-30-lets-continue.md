---
layout: default
title: "lets continue"
---
# lets continue

## Enemy AI
We want to find out the target of the player so the enemies can target the player. When trying to find out the position of a node somewhere in the node tree, groups are used.

In the editor there are two different kind of groups.

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330215541.png)

These are editor only, for better organization. The game itself does not care where the group is placed.

Group names are case-sensitive.

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330215800.png)

Group names are like key value lookups. It is gonna return all nodes in a list that have that group name.

Targeting script (snippet):
```gdscript
...
func aquire_target():
	var players = get_tree().get_nodes_in_group("player") # returns string
	var nearest_player: Player
	var nearest_squared_distance: float
	
	for player in players:
		if nearest_player == null:
			nearest_player = player
			nearest_squared_distance = nearest_player.global_position.distance_squared_to(global_position)
			continue
			# we have not assigned a player, then we assign the first player
			# squared_to because it is less cpu intensive because it does not do a square root calculation
			
		var player_squared_distance: float = player.global_position.distance_squared_to(global_position)
		if player_squared_distance < nearest_squared_distance:
			nearest_squared_distance = player_squared_distance
			nearest_player = player
			
	if nearest_player != null:
		target_position = nearest_player.global_position

...
```

## Creating Health Component / Using Composition

What is composition?
Is the composing of larger chunks of functionality for more modular chunks of functionality.

For example the Main Menu, where the HBoxContainer can be seen as a component that gives me horizontal alignment capabilities.

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330223052.png)

Or for the player, like for movement what the characterbody2D provides, or a sprite node that is added to display graphics.

Every node is a component.

In this case we will create an own node for the health component as godot itself does not have one. This then can be instantiated in scenes which need a health component.

Creating custom signals

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330223759.png)

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330223803.png)

Emit custom signal

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330223832.png)

Then instantiate the health scene:

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330223909.png)

Drag and drop the node into the script as usual

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330224136.png)

Then connect to the signal and reference a new function called "on_died"

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330224130.png)

And free the resource by creating the referenced method

![](/assets/blog/2026-03-30-lets-continue/Pasted image 20260330224247.png)

Healthcomponent script (snippet):
```gdscript
class_name HealthComponent
extends Node

signal died # defining custom signals...

...

func damage(amount: int): # where does amount come from? amount is the damage...
	current_health = clamp(current_health - amount, 0, max_health) # clamp to bypass negative health
	if current_health == 0:
		died.emit()

```

Credit: Firebelley Games (Coop Tutorial, check it out!)
