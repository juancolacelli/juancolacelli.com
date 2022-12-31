---
title: DROID7 v1.1.0
date: 2022-12-20T19:22:00-03:00
description: Big update!
tags: [gamedev]
authors: [jc]
games: [droid7]
---

[DROID7]({{< ref "/droid7" >}}) v1.1.0 release has the following game changes:

**In game changes:**

-   Updated game engine (Godot Engine 3.4.5)
-   Added teleports
-   Added super batteries
-   Added items roulettes, they cycle between all items, so you can choose which one to pick
-   Added walking machines
-   Added different backgrounds per level
-   Changed initial HP from 2 to 4
-   Decreases max HP from 5 to 4
-   Added HP background to show the max HP
-   Improved enemies, now they are angry DROIDs
-   Improved batteries icons
-   Improved batteries effect nullifying other batteries
-   Improved laser graphics and animation
-   Added laser particles when a map element is destroyed
-   Improved boss laser graphics
-   Added pickup animation to items, so you can see what you picked up easily
-   Added skip boss animation
-   Fixed springboards and jetpacks being affected by batteries
-   Rebalanced all map elements
-   Rebalanced all powers durations
-   Improved map graphics, walls and roof will be bigger

**GUI and application changes:**

-   Fixed game over and pause screen overlapping stats
-   Improved splash screen animation
-   Improved game icon
-   Added player powers indicators with icon and duration as a progress bar
-   Added mouse cursor
-   Replaced keyboard/joystick with mouse in game menus movement
-   Improved game menus position
-   Added links in every name on credits screen
-   Removed continue from pause menu, just press pause again
-   Removed score and hi score from game
-   Added laser distance to game GUI
-   DROID7 will look at the cursor in the main menu

**Bug fixes:**

-   Fixed map generation always starting from left to right, making the map easier if you go always left
-   Fixed boss projectiles movement
-   Fixed spikes activating too early, hurting the player too fast
-   Fixed laser cheating, laser will now just increase its speed per level
-   Fixed player being hit while it is on springboards or jetpacks
-   Made several performance improvements
