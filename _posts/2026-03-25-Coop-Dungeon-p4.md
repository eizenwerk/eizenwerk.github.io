---
layout: default
title: "Coop Dungeon p4"
---
# Coop Dungeon p4

I asked AI to explain to me how the multiplayer movement synchronization actually works as I need to understand every Building-Block.

1. When a client connects, they send a peer_ready RPC to the server (main.gd). The server spawns the player instances on all clients via the MultiplayerSpawner Node.
2. Each player has authority over their own **player** as described in main.gd via: `player.input_multiplayer_authority = data.peer_id`. Each players authority = their peer id.
3. Only the client with the authority gathers client input, as can be seen in player.gd: `set_process(is_multiplayer_authority())` and player_input_synchronizer_component.gd: `if is_multiplayer_authority():`
4. In the player scene, MultiplayerSynchronizer is the actual key, It watches the properties we defined and we tell it to sync it through the server to all clients.

![](/assets/blog/2026-03-25-Coop-Dungeon-p4/Pasted image 20260325203540.png)


we removed the set_process function within the player.gd so that the aim direction now gets updated to the client too

![](/assets/blog/2026-03-25-Coop-Dungeon-p4/Pasted image 20260326013010.png)


Credit: Firebelley Games (Coop Tutorial, check it out!)
