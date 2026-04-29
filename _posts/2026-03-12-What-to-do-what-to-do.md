---
layout: default
title: "What to do, what to do"
---
# What to do, what to do

Another fucking shitty annoying ass day in a row. Somehow the time just flies and its late and I was not able to do gamedev. It is not even about procrastinating at this point, I just had things to do all day.
Enough blabbering, I am not gonna waste my streak and I am gonna push trough.

Things we could do today would be the dungeon generator again, but my brain is kinda mushy. So maybe something creative or a video.

I am not sure how to be more creative in regards of the dungeon. I would really love to generate a dungeon (only in cli for now would suffice).

I did the unimaginable and tried to code with sleep deprivation. As expected I couldnt finish it, but im proud for trying and I will continue with that. I didnt ask claude for solutions, only for syntax as I dont know code.

```gdscript
extends Node3D

var array = []
var mapsize = Vector2(3,4)

# Called when the node enters the scene tree for the first time.
func _ready() -> void:
	fill_array()
	print_array()


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta: float) -> void:
	pass

func fill_array():
	for i in mapsize.x:
		array.append("x")
		for j in mapsize.y:
			array.append("y")

func print_array():
	var output = ""
	for y in mapsize.y:
		for x in mapsize.x:
			output += str(array[x])
	print(output)
			
```

Output

![](/assets/blog/2026-03-12-What-to-do-what-to-do/Pasted image 20260313014516.png)

As can be seen the array fills itself the wrong way. Also I need to create a new line after the x values are filled. Before using output to concatenate the string, the array printed one value and went to the next line. 

