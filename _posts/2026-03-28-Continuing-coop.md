---
layout: default
title: "Continuing coop"
---
# Continuing coop

Working on Enemies

Hitboxes are in the players favor? Is that right?

Bullet mask on enemy
Bullet Layer on Bullet

Because collisions need to be handled locally by the enemy?

as this is a multiplayer game we dont want the clients to handle critical things like collision detection

### TYPE CASTING Using functions of custom classes:

![](/assets/blog/2026-03-28-Continuing-coop/Pasted image 20260328200048.png)

I can use functions of custom classes by only defining a variable (here: bullet) as a type of this class, which is the class/type bullet. In this example the function "register_collision" can be used this way.

Alternatives would be to use Singletons (autoloads). Its called autoload because it automatically loads when the game starts, and it is also called singleton as this is the design pattern name (a single global instance).

### Spawn bug
When despawning the enemy when the health is at 0 it does not despawn for the client and does not register any collisions any more.

That is because the Multiplayerspawner does only handle nodes that are spawned through it.

![](/assets/blog/2026-03-28-Continuing-coop/Pasted image 20260328202616.png) 

As can be seen we added the node by hand onto the main scene.

![](/assets/blog/2026-03-28-Continuing-coop/Pasted image 20260328202830.png)

But even if we add the scene resource to the Auto Spawn list of the MultiplayerSpawner we do not get the expected results. Why?

Because the spawner only auto-syncs nodes that are added dynamically at runtime.

Credit: Firebelley Games (Coop Tutorial, check it out!)
