---
layout: default
title: "Recettar inspired Game"
---

# Recettar inspired Game

Todays plan: Watch some 3D related Tutorials and create a recettar inspired game. The Dungeon is 2,5D if i remember correctly.

[https://www.youtube.com/watch?v=ke5KpqcoiIU](https://www.youtube.com/watch?v=ke5KpqcoiIU)

Greyboxing = level blockout

CSG prototyping -> exporting level to blender -> UV mapping?

Snapping size can be set by values:

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307171858.png)

Played some reccetear to understand how the dungeons look and feel like. Tested around with different csg nodes and created a mini dungeon.

Interesting thing, I learned what two buttons do I had to use in multiple tutorials, but never understood why. 

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307232357.png)

When you greybox like I did you will need to create scenes out of building blocks and instantiate them in your main scene. Prototyping is much faster that way, and the change that u fuck up a placed block is much smaller than maybe missclicking on a single wall and falsely placing it somewhere else. Its like guard rails for your process, and if you limit your possible actions, possible problems are scaled down, because with every click the probability of a fuckup increases.

At least that is my justification.

Now about Editable Children and Make Local. Both these options relate to instantiated scenes. When you instantiate a scene within your main scene, the hallway for example, but you need a T-Hallway like I did. You dont want to recreate that from scratch. You check Editable Children, which allows you to edit the children of the instantiated scene within the main scene. But you dont want that. You want to click on Make Local, which allows you to extract the instantiated scene and makes them editable in this scene only. That way you can create a new hallway, and save that as another scene. Now you have the default hallway, and the T-hallway which is based on the normal one, but is not dependant on it. It is his own instance.


Final Result after 2h

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307231935.png)

Hallway

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307232742.png)

T-Hallway (Hallway-derivative)

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307232811.png)







![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307171649.png)
("Recettear: An Item Shop's Tale" - inside the dungeon)

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307173141.png)
("Recettear: An Item Shop's Tale" - city map)

Map Music man... awesome

Also, I really like this asthetic

![](/assets/blog/2026-03-07-Recettar-inspired-Game/Pasted image 20260307233338.png)

I guess the reason it looks so good is, after evey hit time slows down and the camera zooms in? And if one gets hit the camera shakes?









