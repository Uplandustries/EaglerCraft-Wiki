---
title: Play Experience
description: 
published: true
date: 2026-01-09T07:03:22.398Z
tags: 
editor: markdown
dateCreated: 2026-01-07T15:38:23.412Z
---

# Play Experience
#### In development - Please excuse any missing information

# Resource Packs
Despite popular belief, Resource Packs[^1] do NOT increase your framerate. What they can do, is stop your frames from dipping and/or fluctuating, but they cannot increase your framerate directly. This solely relies on your settings and your hardware's performance.

You can find resource packs at some of the following places:
https://resourcepack.net/
https://modrinth.com/resourcepacks
https://resourcepacks.gg/en
https://resourcepacks24.de/

> Make sure you are using a trusted site before downloading any kind of file, not just resource packs.
{.is-warning}


***TODO: Should we add some recommended resource packs here?***

# Optimal settings
For low performance machines (most likely chromebooks), it is best to keep your settings low unless using a performance enhancing client, such as the ones listed in the *Eaglercraft Clients* page. For higher end machines, you can pretty much do whatever you want.

Eaglercraft has built in shaders, you can turn these on by navigating to Pause Menu > Shaders. These will significantly hit your performance on Eaglercraft, so it is recommended to keep these off unless you really want shaders.

When using the WASM (WebAssembly) version of Eaglercraft, please make sure that you keep Vsync enabled, or your frame buffers will not update in time, causing drops in performance significantly, even if your framerate says it's higher.

You can keep VSync disabled on the JS version, as this only applies to the WASM builds.

---

Alright, now let's get to it. Here are the optimal[^2] settings for Eaglercraft 1.8.8 JS:
 -  Graphics: Fast
 -  Smooth Lighting: OFF
 -  VSync: OFF
 -  Clouds: OFF
 -  Particles: Minimal
 -  Fog: OFF
 -  Entity Shadows: OFF
 -  Render Distance: 6 chunks[^3]

Although these settings are highly recommended, you may be able to get away with having Clouds, Fog and/or Particles set to ON. You may also be able to set Graphics to Fancy or Smooth Lighting to Minimum, but you may want to lower your render distance.

# Causes of Lag
The are 3 main types of lag that will effect your playing experience with Eaglercraft: **client, server, and connection lag**.
## Client lag
Client lag is the most obvious type; it's when your framerate (FPS) noticably drops. 

The main cause of a lower FPS is having a lot to render. A high render distance or enabling shaders commonly decrease FPS. Also, a ton of mobs being present, which have more complex geometry than normal blocks, will have an effect. Speaking of blocks, ones with complex shapes such as chests may also cause client lag.

Having lots of tabs open can also have a huge effect on client performance. Extra tabs can fill up RAM, which if full, overflows to your hard drive, causing the CPU to wait significantly longer and slow to a crawl (very common on low-end school Chromebooks). Also, extra tabs cause an increased CPU usage in general, which can slow down your game.

## Server lag
Server lag occurs when the TPS[^4] of the server drops below 20. This occures when the main tickin threads takes more than 50ms to process a tick.

> Some tasks may not be effected by server lag as much because of multi-threading. Not all servers do this and not all tasks use seperate threads. An example of this is the chat on Paper servers. Even if the main ticking thread is slowed down, the chat keeps chugging along!
{.is-info}

#### Loading chunks
When players move around, chunks have to be loaded from region files on your hard drive to RAM. This process is very CPU intensive. If a system's CPU has enough cores/threads, this may not cause issues (on most servers), however if a system doesn't, it may cause the world ticking thread to slow down.

Once chunks are loaded into RAM, they all must be processed constantly by the server's ticking thread. The more players you have with loaded chunks, the slower this can become.

#### Entities
Entities tend cause a lot of lag on the main ticking thread due to collisions, pathfinding, and other AI tasks. Of course, the more chunks are loaded (see above), the more entity ticking can be a problem.

There are many plugins out there to remove, stack, and/or remove AI from entities. There are many plugins such as [WildStacker](https://www.spigotmc.org/resources/%E2%9A%A1%EF%B8%8F-wildstacker-%E2%9A%A1%EF%B8%8F-spawners-entities-drops-blocks-%E2%9A%A1%EF%B8%8F-1-21-10-support.87404/) and [LagFixer](https://modrinth.com/plugin/lagfixer) that seem to stay up-to-date, but there are many others on [Modrinth](https://modrinth.com/discover/plugins), [CurseForge](https://www.curseforge.com/minecraft/search?class=bukkit-plugins), [SpigotMC](https://www.spigotmc.org/resources/categories/spigot.4/), etc.

#### Plugins

Ironically, having many of those lag managment or other plugins can itself cause lag. Plugins that use the Scheduler for complicated tasks may have code that runs in different threads, however not all plugins do, and a server with few cores/threads may still struggle.

## Connection Lag
Connection lag occurs when you client doesn't have a good connection the the server (or maybe the relay for shared worlds).

If everything stops moving, you can't open inventories (such as chests), and the chat stops moving, you may be experiencing connection lag.

Switching tabs can sometimes cause your connection to drop out; this takes a moment to update, causing everything to freeze and suddenly disconnecting you.

> It is also the cause of the infamous "End of stream." message that *everyone* has experienced at some point.
{.is-info}

Another common cause of connection lag is a bad Wi-Fi signal, and your client loading lots of chunks at once on a bad signal can compound he issue.

> Try lowering your render distance.

High server load or client lag can also contribute to connection issues, causing this type of lag to be hard to diagnose in many situations.

---

[^1]: Sometimes called Texture Packs - different from Data Packs
[^2]: Tested on a Dell Chromebook 3110, should apply to most other models.
[^3]: 6 chunks should work perfectly for most devices but may lag on certain devices, use 4 (or less but the experience isn't great) if needed.
[^4]: Ticks Per Second. The target tick rate (in most cases) is 20: if it takes more than 50ms to calculate each tick (MSPT), the server is lagging.