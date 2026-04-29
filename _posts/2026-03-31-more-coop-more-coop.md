---
layout: default
title: "more coop more coop"
---
# more coop more coop

## Global Signals

At the time we dont advance rounds. We need to fix that.

Autoloads will be used this time.

When to use autoloads? When data/systems need to persist across multiple scenes AND need to be accessed from anywhere in the game.
Everything else is a custom class.

Examples for autoload
- Player inventory
- UI Manager
- Settings
- Achievement/Trophy systems

Examples for classes
- Single NPC with dialogue
- Animation for a character
- Particle effect for an explosion
- Enemy AI pathfinding
- World manager (restart level etc)
- Projectile/Bullets

After you have added a autoload in the project settings, when the game runs, the node gets automatically added to the scene tree with its script attached. 

![](/assets/blog/2026-03-31-more-coop-more-coop/Pasted image 20260401004202.png)

![](/assets/blog/2026-03-31-more-coop-more-coop/Pasted image 20260401004214.png)

And then just call it from anywhere:

![](/assets/blog/2026-03-31-more-coop-more-coop/Pasted image 20260401004445.png)

Now we check if the round is completed and enemies are left OR if all enemies are dead before the timer is stopped.

## Hurtbox and Hitbox

We want to streamline things that get damage or make damage. But we also need to damage the player, which we current dont have.

Hurtbox-component: Receives damaging collisions

Hitbox-component: Contains the data about the damaging collision

## Warnings

![](/assets/blog/2026-03-31-more-coop-more-coop/Pasted image 20260401011524.png)

You can ignore them. But there could be potential errors.

These warnings can be configured in the project settings

![](/assets/blog/2026-03-31-more-coop-more-coop/Pasted image 20260401011646.png)

- supress delta warnings with an underscore
- rename variables when shadowing (reusing names of existing properties)
- adapt randi to randf when having precision loss
- etc

Credit: Firebelley Games (Coop Tutorial, check it out!)
