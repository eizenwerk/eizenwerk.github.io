---
layout: default
title: "Prototyping for a gamejam"
---

# Prototyping for a gamejam

Also, that looks good, someone posted that on jackes discord:

![](/assets/blog/2026-02-26-Prototyping-for-a-gamejam/Pasted image 20260226153945.png)

Looks very similar to my plans? But thats maybe a coincidence. Wouldnt matter if its the same place though.

Also this, which seems to be UV unwrapping. I have to look into that:

![](/assets/blog/2026-02-26-Prototyping-for-a-gamejam/Pasted image 20260226154812.png)

Lets get back using the kenneys prototype, importing them manually.

Textures (in this case kenneys prototype textures, available as png files) get applied via a **Material**. The chain is: **Texture -> Material -> Mesh**

For Prototyping in Godot, CSGShapes are recommended. These are more resource intensive during gameplay, and are therefore not recommended in the final build.

Why? Because boolean operations are calculcated every frame on the cpu and not on the gpu.

I then started prototyping and this is not as brain-intensive as learning theory or programming. I can understand simple building blocks and subtracting them from each other. Very intuitive, but somewhat complicated or limited when u want to do something more complicated, like the satellite dish on the roof.

![](/assets/blog/2026-02-26-Prototyping-for-a-gamejam/Pasted image 20260227112119.png)

![](/assets/blog/2026-02-26-Prototyping-for-a-gamejam/Pasted image 20260227111810.png)

![](/assets/blog/2026-02-26-Prototyping-for-a-gamejam/Pasted image 20260227111815.png)

The main problem during creation was one thing. I was not able to feel if walls are to high, if doors are to narrow etc, as I didnt use 1x1 blocks which equal to 1x1 meters. I wanted to do that but the main reason was that every csg block that I copy uses extensive ressources. I had like 500 csgs and the editor started to lag, and that was just the floor. I then had the idea to use a single csg and just scale it up. With Triplanar and World Triplanar set, scaling does not effect the texture.

![](/assets/blog/2026-02-26-Prototyping-for-a-gamejam/Pasted image 20260227112414.png)

