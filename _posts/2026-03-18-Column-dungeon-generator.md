---
layout: default
title: "Column dungeon generator"
---
# Column dungeon generator

![](/assets/blog/2026-03-18-Column-dungeon-generator/Pasted image 20260417000232.png)

- create array
- define zones
- fill random cell for every column and every type (S, B, F, D)
	- (S)pawn
	- (B)ossroom
	- (F)ocuspoint
	- (D)istractionRoom
- Connect cells and fill cells with (P)ath -> math and looping lol
- Connect (D)istractionRooms to path in their Column (or radius for randomness)

I currently have problems with choosing the x colum ranges when choosing a random cell. 

I dont understand this, i have to look further into this tomorrow.

![](/assets/blog/2026-03-18-Column-dungeon-generator/Pasted image 20260319005402.png)

This was bullshit. Too much refactor. This is much cleaner now.

![](/assets/blog/2026-03-18-Column-dungeon-generator/Pasted image 20260319010153.png)

The reason it was that bullshit complicated was, that we called the place cells function twice, once in ready and once in the create path function. This fucks up the loop. A quick and easy fix is just to call the function only once within the function where it is needed, that way we can use the return values, as a function needs to be called before return values can be used, obviously.

Another way would be to call it in ready and just store the values in a class variable (a variable at the top outside of every function, therefore there wont be any scope issues)

