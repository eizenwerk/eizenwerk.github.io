---
layout: default
title: "coop state machines"
---
# coop state machines
### Callable

![](/assets/blog/2026-04-22-coop-state-machines/Pasted image 20260422234640.png)

Why would we use a callable? But sometimes we dont know which function to call until later. An example could be a button, that does different things depending on the situation.

```gdscript
func on_button_pressed():
    if mode == "save":
        save()
    elif mode == "quit":
        quit()
    elif mode == "open_menu":
        open_menu()
```

With a callable, we just store which funciton to call ahead of time.

```gdscript
var action: Callable

# somewhere you set it
action = save
# or
action = quit

# button just does this, no if/else needed
func on_button_pressed():
    action.call()
```

A special case for that are signals. We alreadu used callables in them.

```gdscript
func _ready():
	button.pressed.connect(on_button_pressed)
	#                      ^^^^^^^^^^^^^^^^^
	#                      THIS is the Callable
```

As you know you connect to functions in the ready method, which is only run once when the node is ready. But how is it able to listen for signals when we do not check every frame, why dont we put the connection in the process function? Because we **store** it with the callable. 
But here we do not use **callable** written out, we use the name of the function that is called when the button is pressed. Here is an example of explicitly using the **callable** constructor, we pass it two things:

```gdscript
var c = Callable(self, "on_button_pressed")
button.pressed.connect(c)
```

It is the same thing as before, just written out manually.
1. We pass the object the method belongs to - usually **self**
2. The method name as a string
3. When the button is pressed, c is run.

Credit: Firebelley Games (Coop Tutorial, check it out!)
