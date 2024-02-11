---
title: Teleporting extremely slowed down my game
date: 2024-02-10
---
A while ago, when I implemented teleportation in my game, I saw something strange happening. The further away the destination was, the longer it took to perform the teleportation and the game would appear to freeze while doing it. At some point, it took like 1-2 seconds on my (rather performant) desktop PC.

After a while I figured that this might be due to colissions happening on the path between the origin and the destination. So, when I disabled colission detection during the teleportation, the teleportation happened instantaneously!

This means that the more collidable nodes there are on the path to the destination, the more work the Godot engine has to do to handle colissions with them.

Here's some code that shows how to easily teleport a node without causing intermittent colissions:

```csharp
// Keep a copy of the colission bits.
var originalCollisionLayer = CollisionLayer;
var originalCollisionMask = CollisionMask;

// Clear the colission bits to disable colission detection for the node.
CollisionLayer = 0;
CollisionMask = 0;

// Teleport somewhere far away.
Position += new Vector2(5000, 8000);

// Restore the colission bits to enable colission detection again.
CollisionLayer = originalCollisionLayer;
CollisionMask = originalCollisionMask;
```
