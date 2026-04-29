---
layout: default
title: "Continuing dungeon generation"
---
# Continuing dungeon generation


Seems like i have issues with my current algorithm:

![](/assets/blog/2026-03-17-Continuing-dungeon-generation/Pasted image 20260317034618.png)

Another dungeon generator apporach i would like to implement:

![](/assets/blog/2026-03-17-Continuing-dungeon-generation/Pasted image 20260417000232.png)

- create array
- define zones
- fill random cell for every column and every type (S, B, F, D)
	- (S)pawn
	- (B)ossroom
	- (F)ocuspoint
	- (D)istractionRoom
- Connect cells and fill cells with (P)ath -> math and looping lol
- Connect (D)istractionRooms to path in their Column (or radius for randomness)

---


asonchrynous multiplayer


