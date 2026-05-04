---
layout: default
title: "Thoughts about composition"
---
# Thoughts about composition 

I thought about composition in godot and realized that I dont have a real understanding of its workflow. So lets have a quick chat about it.

We focus on two game engines, unity and godot. Unity, because when i started playing around with it, it felt natural and convenient to me. And to be honest if the compile time would have been like with godot (as I am constantly changing values and testing stuff in the beginning, because I am learning), I would have stayed and even learned c#. But the loading times fucked me over so I decided to go with godot.

Lets talk about the structural difference between both engines. Nodes vs Components philosphy. Both engines use hierarchical scene structures with parent-child relationships. You have a main or starter scene, you have children which inherit properties like the rotation or the position.

Unity uses a component-based system. You attach components to Gameobjects. The hierarchy is optional. To make one Gameobject talk to another, you have to reference them in code.
Godot uses the node-based system. Every node has its own built-in behaviour. These nodes are nested into each other, where the hierarchy defines the relationship. Communication between these nodes is done via signals that flow through the node tree.

Watch this video to get a good overview, the first half is pretty recommendable:
[https://www.youtube.com/watch?v=e3H_nw4w5U8](https://www.youtube.com/watch?v=e3H_nw4w5U8)


