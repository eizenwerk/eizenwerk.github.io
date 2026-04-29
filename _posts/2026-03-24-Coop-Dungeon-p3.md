---
layout: default
title: "Coop Dungeon p3"
---
# Coop Dungeon p3

Problem: When me move a player we move all players. But players need authority over their own instance and replicate the movement on the other peers.

? How does the server make sure that the input is not maliciour or correct?

! There is a delay because of the roundtrip latency

MultiplayerSynchronizer: Syncs properties from the authority to the remote peers. In our case we give authority over the movement to themselves.

This we want to sync from the player.gd script
```gdscript
	var movement_vector = Input.get_vector("move_left","move_right","move_up","move_down")
```


Credit: Firebelley Games (Coop Tutorial, check it out!)
