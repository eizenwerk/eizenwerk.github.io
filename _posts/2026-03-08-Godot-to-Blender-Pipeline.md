---
layout: default
title: "Godot to Blender Pipeline"
---
# Godot to Blender Pipeline

As I have my prototype level figured out, it is now time to export them to blender and UV map them. As far as I understand I can assign textures that way, which is needed for my recettear dungeon inspired game.

Select the scene with the building block you want to edit in blender and export it to gltf:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308221314.png)

Dialog window appears, I left everything at default:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308221751.png)

After that, import the gltf file into blender.

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308221728.png)

Go to the shading tab:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308222851.png)

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308222908.png)

If you can remember I assigned a black color to the mesh because I wanted better visibility when prototyping the dungeon. This black color wasnt assigned to the areas where a substraction was done. This is no issue, as you can just select these different areas in blender and assign any texture you want.

Add an Image in the bottom part, by clicking shift+A:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308223112.png)

Search for Image:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308223124.png)

Connect Color to Base color:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308223200.png)

Open and find your texture png file:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308223237.png)

My Mesh now looks like this:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308234924.png)

Switch to edit mode by pressing TAB.

Select Face:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308235123.png)

If you now want to texture individual faces you can select the face like i did by clicking on the triangles within the face:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308235155.png)

Now select Material in the properties tab on the right side (1), select your material (2) and assign it(3).

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308235411.png)

The result should look like this:

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260308235420.png)



End result after exporting it to godot again.

![](/assets/blog/2026-03-08-Godot-to-Blender-Pipeline/Pasted image 20260309004551.png)

IMPORTANT: When you rename the png you imported, it wont show it in blender. You will see it when you import the new glb to godot and it has no textures.

