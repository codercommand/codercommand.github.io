+++
title = 'Arcade: Extended GDD'
date = 2024-04-30
draft = false
+++

Copyright, Rian Rutherford, 2024, All rights reserved.

_This is a live document and continues to have edits._

![Image](../arcade-gdd/gavin-rothery-concept-piece-8-colour-schemes-black-v006.jpg)
> ^ Concept art by Gavin Rothery [source](https://www.artstation.com/artwork/bKXE2G).

# GDD Extended

This document originated as an extended section in the GDD. From 30th April 2024 it has been separated into its own document. While this has already been published, it is a live document and will continue to receive edits.


# Weapons Ideas

All most projectiles should be slow enough that a player has enough time to react, turn 180 degrees, and shoot it down with another projectile.


##### Standard Missile

Scans for a target and chases the closest target. This includes other missiles, not just spaceships. The missile does medium damage to the target it hits. This missile does not have AOE damage.


##### Micro Nuke Missile

Scans for a target and chases the closest target. This includes other missiles, not just spaceships. The missile explodes in an AOE when destroyed by another missile, reaches the end of its life, or hits a target. The missile does huge damage to everything in an AOE. The missile is slower than most others.


##### Triple Missile

You shoot a missile that breaks into 3 smaller missiles, each doing 1/3 the damage of a standard missile. The missile and smaller missiles have the same behavior as the _Standard Missile_.


##### Cloud Rocket

A missile that shoots in a straight line, if it detects a missile in it’s range it will explode creating a smokescreen This smoke screen stops missiles from tracking their target while inside the smoke. Missiles in the smoke tranvel straight till they leave.


##### Rocket Barrage

The player can shoot lots of small rockets like a machine gun or rocket pod. These rockets have poor turning making them bad at hitting targets suddenly changing directions. 

{{< youtube N4JhkjtCnVQ >}}


##### Gravity Void Missile

A missile that creates a gravity void sphere (like a black hole) when it’s near an enemy spaceship or missile. It lingers in the area for a long period of time, and pulls stuff towards it. It does not cause damage to anything it pulls in. The gravity void is intended as a type of crowd control ability and large AOE map control ability.



# Level & Environment Design Ideas

##### Moving City/Moving Ground

When close to the ground as you move above it, structures will appear out from the ground in front of you and disappear again behind you.

Specifically the structures will achieve this by moving up and staying out fully extended a second or two before the player moves past them, then will move back down into the ground.

One variant idea of who this moving ground could be as you fly over a desert, the sand jumps to form pillars or other shapes when you’re near the ground. The plot/logical reasoning is because the sound bounces from the acoustic sound of the spaceship, example:

{{< youtube Q3oItpVa9fs >}}


##### Multi Atmosphere

Levels can have multiple atmospheres with different amounts of air friction/air density.

1. Space no friction
2. High altitude low friction
3. Low altitude high friction
4. Water/Other extreme friction

The friction in the air could also scale with a gradient or use a curve graph to have a wide array of frictions at different altitudes scaling differently.


##### Fog Level

Foggy level where fights look like lots of small dots flashing in a cloud.



# Target Audience

The games competitors are games that feature multiplayer spaceship combat targeting audiences that aren't looking for action gameplay instead of a 1:1 space simulator.

Out tags include: Multiplayer, PvP, Sci-fi, Action, Space, 3D, Spaceships. Using all these tags doesn't reveal all our competitors, you must use different combinations to get a feel for what's out there. [SteamDB](https://steamdb.info/instantsearch/) was used to search for competition.

Found competitior games:
1. [In The Black](https://steamdb.info/app/380110/) The game is in development by [Impeller Studios](https://impellerstudios.com/). Its target audience are people looking for hardcore PvP spaceship combat. While we share a similar audience, our combat and movement are fundamentally different. Because of this we share some of the target audience, but are not in direct competiton tying to provide the same game.
2. [Star Age: Space Combat](https://steamdb.info/app/1726690/) is an already release game with no playerbase. It's a dead game, quick google search and the only YouTube video available is a trailer. While they're arcade like with simple controls and thirdperson camera, they do not share our design pillars or target game qaulity on release.