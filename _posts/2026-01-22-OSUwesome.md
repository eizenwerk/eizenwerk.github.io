---
layout: default
title: "OSUwesome"
---
#beatgame
#blog

I got a youtube video for osu recommended and as I want to get inspired I looked into it. This interface feels so smooth and awesome. I typed in my name and the animation was on peak. Like this:

![](/assets/blog/2026-01-22-OSUwesome/Pasted image 20260122203324.png)
 
When starting the game it asks for beatmaps, as the game itself does not come with them. What are beatmaps?
Beatmaps are gameplay levels, configured manually by players, that synchronize visual objects to a songs rythm. When you create an OSU account, you can download such a beatmap. 

![](/assets/blog/2026-01-22-OSUwesome/Pasted image 20260122201433.png)

![](/assets/blog/2026-01-22-OSUwesome/Pasted image 20260122201451.png)

The osz file itself can be unpacked with 7zip for example. Contents are different beatmaps, the thumbnail and the song itself.

![](/assets/blog/2026-01-22-OSUwesome/Pasted image 20260122201537.png)

The osu files are human readable. If we skip to the Timingpoints, we can see what values OSU needs to work.

![](/assets/blog/2026-01-22-OSUwesome/Pasted image 20260122201708.png)

For us, the only two important things are the first and second value. The offset "712" and the beat interval or BPM "333.33...". The game does not hardcode every beat at every possible time, it defines an offset and the BPM, and then a new increased or decreased BPM at a new offset, which in this case is 8868.

Beatmaps are a lot of work, but I guess the developers wanted the players to have fun. More songs, more fun. Especially when you can play around with songs you are already familiar with.

Also there seems to be [https://beatconnect.io/,](https://beatconnect.io/,) which is a mirrorsite for OSU beatmaps. Best possible option would be to allow and support osu beatmaps as they already exist, which then can be imported directly. Also creating an own beatmap editor in the game where players can create their own beatmaps (I personally dont like the extra manual work people have to do, but I like the technical challenge of implementing a beatmap editor). Another option would be an Implementation of a constant BPM for songs or hardcoded beatmaps - which sounds aweful. Maybe some combined approach is the correct way of doing it.

As usual, music is a shitshow in regards of licensing. No one is allowed to use osu beatmaps when these songs are protected. But it is allowed to read OSU files when the music is not licensed, when prohibiting users from importing licensed music. One could go the safe crypt of the necrodancer approach, and only allow local music files. That prohibits sharing of music. But also kills the community. But for the music industry, OSU is not a target because they take down copyrighted content (which is totally justified) and its non-profit status... which doesn't work for paid games published on steam.

Disclaimer: I’m not a lawyer - these are simply my personal notes, so please verify the legal details on your own.

More infos:
[https://osu.ppy.sh/wiki/en/Client/File_formats/osu_(file_format](https://osu.ppy.sh/wiki/en/Client/File_formats/osu_(file_format))

