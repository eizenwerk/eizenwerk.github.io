---
layout: default
title: "Dungeon Generation"
---
# Dungeon Generation

Im really tired today, so lets focus on something "passive". I got a dungeon generator video recommended and I am gonna watch that and make some notes.

[https://www.youtube.com/watch?v=gHU5RQWbmWE](https://www.youtube.com/watch?v=gHU5RQWbmWE)

- Create the rooms
- Assign walls and doors at the same place, i guess that they are enabled or disabled by the generator
- Name doors based on the orientation, a la top, left, down, right

code

- create array out of door, 0 is up, 1 is down etc
- function that checks if doors are open or closed, it checks the index for true or false, true means there is a door for the specific index entry
- function for loops through the index and sets them active and sets walls inactive, just as I guessed before
- generation of the dungeon: Depth First Search algorithm, creates a maze, it randomly picks a cell until it goes through all possible unvisited cells until it has nowhere else to go, then it goes back and tries to find all possible paths  ![](/assets/blog/2026-03-11-Dungeon-Generation/Pasted image 20260311233724.png)
- First step is to choose a starting cell
- Class Cell that contains information of all cells, it has to check if the cell has been visited or not
- Class Cell that checks the status of the cell, checks for doors
- Create a function that creates a maze
- Create a function that checks neighbours



ideas for dungeon generation
- create x rooms based on the level difficulty or level
- find paths between the rooms, test if every room is reachable and the boosroom is reachable
- at the end of every path there should be a door, paths shouldnt aim towards nothing


--- godot specific video

[https://www.youtube.com/watch?v=yl4YrFRXNpk](https://www.youtube.com/watch?v=yl4YrFRXNpk)

![](/assets/blog/2026-03-11-Dungeon-Generation/Pasted image 20260311234259.png)

Pre watch ideas, how would this one work?

- Path that goes from start to end
- Branches out a couple of times and continues a little along the main path
- Create a grid
- Find a starting position
- define and ending position by random (define min distance)
- find path (i guess vector math? Or some algo? My guess would be divide the distance by 3, create a path that does not go the shortest distance, have three tracks where the position of every branch is choesen randomly within these tracks, go into a random direction with a min distance and try not to overlap with other ways, randomly go in another direction by randomly choosing vector x or y )

video:
- Constraints: Maximum size of the dungeon a la dimensions like 5 wide, 7 long -> array
- loop through the x and y dimension to create an array with the size of the dungeon and set (initialize) 0 for every index entry
- print, go through x first,, add one y, next x line, print with new line, prototype in the cli first before using meshes ![](/assets/blog/2026-03-11-Dungeon-Generation/Pasted image 20260311235114.png)
- Set static start position for the dungeon, if not valid, randomize starting position
- Set array position to S for start position
- Set ciritcal path length = minimum path distance
- Create function that generates critical path
- This function randomly chooses a direction 1-4 and switch cases the direction
- Check if the direction is out of bounds OR is not empty , rerandom direction
- if direction is ok, change value +1 direction
- use starting point values as reference when calculating the critical path,
- every loop, add 1 for every loop step after moving to the reference point length until defined length is met

