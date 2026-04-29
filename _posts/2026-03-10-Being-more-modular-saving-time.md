---
layout: default
title: "Being more modular, saving time"
---
# Being more modular, saving time

How to apply the texture on the floor and scale it:

Assing a StandardMaterial3D to the node

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260310234414.png)

Open the Material, open the Albedo setting and drag the texture you want onto the Texture field

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260310234528.png)

As you can see texture is stretched over the whole node.

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260310234559.png)

Just go to UV1 to change the scale

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260310234646.png)

Voila

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260310234737.png)

Now lets repaint the walls and doors in Blender and add them to the scene, then rebuild the scene.

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311004456.png)

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311004938.png)

We then reeimport these glb files into godot and replace the basic building blocks wall and door.

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311013052.png)

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311013106.png)

Now we can rebuild all rooms we built before out of these building blocks.

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311013137.png)

Godot is gonna error that there is not collision shape. But the instantiated scenes (walls and doors) all have collision shapes, so we can ignore this.

In the scene, with some green directional light, fog and the texture on the ground plus the replaced modular blocks the level now looks like this:

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311013016.png)

![](/assets/blog/2026-03-10-Being-more-modular-saving-time/Pasted image 20260311013019.png)

