---
layout: default
title: "Website and FSM (again)"
---
# 2026-04-25 | Website and FSM (again)
The last couple of days I was invested in creating a public appearance. I have enough notes to fill it, and I guess this was the most difficult for me in the past. There is no need to build a blog if there is no content, right?

So how was this website built? It uses github pages and jekyll. I used the jekyll minimal theme as a base as I found it the most visual pleasing. It should focus on the most important thing, the content itself. And it should be convenient to use. After a couple of days playing around with it I am now happy with what I have built. It has a search funktion, the logo looks good, every post does generate a thumbnail and fallbacks to a default image if no image is part of the post. It even scales properly on mobile. Even though I invested a lot of time in the last couple of days, I do not count this as progress for my daily godot streak.

Light mode
![](/assets/blog/2026-04-25-Website-and-FSM-(again)/Pasted image 20260426044747.png)

Dark mode
![](/assets/blog/2026-04-25-Website-and-FSM-(again)/Pasted image 20260426044805.png)

Scaling for mobile and windows with narrow width
![](/assets/blog/2026-04-25-Website-and-FSM-(again)/Pasted image 20260426044859.png)

# FSM

Ive read up on the basics of FSM and even though I get the concept, the tutorial I am following right now uses code I am not very familiar with. My aim is to be able to understand every single line of code and be able do explain it. So I have taken the callable_state_machine.gd from the tutorial im working on and I will explain the different functions and parts it uses to get an understanding how this FSM works.

## add_states()

```gdscript
var state_dictionary = {}

func add_states(
	normal_state_callable: Callable,
	enter_state_callable: Callable,
	leave_state_callable: Callable
):
```

Here, we create a function called "add_states" and define three parameters of the type Callable. All three parameters are required every time you call add_states().

add_states is called once per state. Each call adds one state to the dictionary. So if your character has 5 states, you would call add_states 5 times during setup, then call set_initial_state once to pick the starting one.

```gdscript
func set_initial_state(state_callable: Callable):
	var state_name = state_callable.get_method()
	if state_dictionary.has(state_name):
		_set_state(state_name)
	...
```

Lets imagine we have 3 states (idle, run and jump) and the script runs. The filled dictionary would then look like this:

```gdscript
{
    "idle": {
        "normal": <Callable: idle>,
        "enter": <Callable: enter_idle>,
        "leave": <Callable: leave_idle>
    },
    "run": {
        "normal": <Callable: run>,
        "enter": <Callable: enter_run>,
        "leave": <Callable: leave_run>
    },
    "jump": {
        "normal": <Callable: jump>,
        "enter": <Callable: enter_jump>,
        "leave": <Callable: leave_jump>
    }
}
```

This is a dictionary of dictionaries (nested). The outer keys are state names (idle, run and jump). Each value has a smaller dictionary with three fixed keys called normal, enter and leave.

## func set_initial_state()

``` gdscript
func set_initial_state(state_callable: Callable):
	var state_name = state_callable.get_method()
	if state_dictionary.has(state_name):
		_set_state(state_name)
	...
```

This function sets the initial state. It takes one input, and we are going to call that input state_callable, which must be of type Callable.
This parameter is like an empty box with a label on it. The value that goes into the box is whatever the caller passes in. So if we call this function somewhere in another script, we would write something like this, which passes the parameter "idle":

```gdscript
state_machine.set_initial_state(idle)
```

Which then:
1. Runs the function set_initial_state
2. The parameter state_callable gets filled with the value "idle"
3. Inside the function body, everytime we see state_callable, we are referring to that idle function

But what happens in the next line when we `var state_name = state_callable.get_method()`? Since when are we able to assign functions to a variable? Since always. In GDScript, functions are values. Just as we can store strings or numbers we can store a _reference_ to a function in a variable. The type for a variable holding a function reference is <mark>Callable</mark>. So when we see `var state_callable: Callable`, that variable is holding a function. Not the result of running the function but the function itself. Ready to be run when we need to.

This is why the state machine works. The dictionary does not hold results of idle, it stores functions. Then later, when the machine runs them, it grabs them out of the dictionary and calls them.

But since when does state_callable have a method? We run `get_method` on the state_callable, so it has to have one, right? State_callable does not have a method by itself. But <mark>Callable</mark> is a built-in Godot type, which has baked methods into it. These methods operate on the function _reference_ itself. Some of these built-in methods for <mark>Callable</mark> are:

`.get_method()` - returns the name of the function as a string, not a method!
`.call()` - actually runs the function
`.is_null()` - checks if the callable is empty

So `state_callable.get_method()` is asking: "What is the name of the function you are holding?" Which answers with the string "idle".

A lot of "overcomplicated" syntax, but there are a couple of reasons to do so. The main reason is, yes you could put a literal string into the function parameter like this:

`state_machine.set_initial_state("idel")`

Which contains an error, that godot can not detect. If it is of type <mark>Callable</mark>, like here:
 
`state_machine.set_initial_state(idel)`

But we will get an error at parse time, as godot detects that there is no function called "idel". So Type casting is the main reason to have this "overly" complicated syntax.

## func update()

```gdscript
func update():
	if current_state != null:
		(state_dictionary[current_state].normal as Callable).call()
```

`dict.normal` means the same as `dict["normal"]` in godot. Its just another way of writing it.
Which means, if we can also use:

`(state_dictionary[current_state]["normal"] as Callable).call()`

This seems easier to read and understand right? Because now we understand that this is a nested dictionary. Then we use `as Callable` to use type casting, which tells godot to treat this value as a <mark>Callable</mark>. This is important so that `.call()` works without warnings. It would run either way, but using type casting is a best practice we should use.

Finally, `.call()` runs the function which is stored under "normal" for the current state. If the current state is "idle", it runs the idle function. The dictionary lookup decides which one is chosen, `.call()` then executes whatever came out.

![](/assets/blog/2026-04-25-Website-and-FSM-(again)/Pasted image 20260427025057.png)

In the end, we check if there is a current state, lookup the normal key for the current state entry in the dictionary and run the function within it.

## func change_state()

```gdscript
func change_state(state_callable: Callable):
	var state_name = state_callable.get_method()
	if state_dictionary.has(state_name):
		_set_state.call_deferred(state_name)
	...
```

When the function gets run, for example with `change_state(run)`,  this function takes the name of the Callable passed in, which is "run" and assigns it to `state_name`. It then checks if "run" exists as key in the `state_dictionary`. If it does, it schedules to run the function `_set_state` with the state_name "run" at the end of the current frame. If it does not, it prints a warning.

## func _set_state()

```gdscript
func _set_state(state_name: String):
	if current_state:
		var leave_callable = state_dictionary[current_state].leave as Callable
		if !leave_callable.is_null():
			leave_callable.call()
	
	current_state = state_name
	
	var enter_callable = state_dictionary[current_state].enter as Callable
	if !enter_callable.is_null():
		enter_callable.call()
```

To understand this function we are gonna use an example and are calling `change_state(run)`, as we are coming from the "idle" state. As `change_state()` is passing the `set_state` function the string of the next state, we can continue working with this new state. Lets imagine the `change_state()` function only gets called when changing states is intended.

So if the current_state variable holds data, which was first filled by `set_initial_state()` at startup and is updated by `_set_state()` itself on each switch, we assign `leave_callable` the function in the nested dictionary entry `["idle"]["leave"]`. If `leave_callable` contains data aka a function, we call the function.

Then, the `state_name` which is currently "run", gets assigned to `current_state`

Afterwards, we assign `enter_callable` the function from the nested dictionary entry `["run"]["enter"]`.

Finally, we almost do the same as before, as we run the function assigned to `enter_callable` if it contains data (here, a function).


Credit: Firebelley Games (Coop Tutorial, check it out!)
