---
title: Teleporting
date: 2024-02-10
---
A while ago, when I implemented teleportation in my game, I saw something strange happening. The further away the destination was, the longer it took to perform the teleportation and the game would appear to freeze while doing it. At some point, it took like 1-2 seconds on my (rather performant) desktop PC.

After a while I figured that this might be due to colissions happening on the path between the origin and the destination. So, when I disabled colission detection during the teleportation, it happened instantaneously!

So this means that the more nodes that can collide with the node you are teleporting there are in the path to the destination, the more work the Godot engine has to do to handle them and this can add up to a lot of work!

Here's some code that shows how to do this easily:

```csharp
// Keep a copy of the colission bits.
var originalCollisionLayer = CollisionLayer;
var originalCollisionMask = CollisionMask;

// Clear the colission bits.
CollisionLayer = 0;
CollisionMask = 0;

// Teleport somewhere far away.
Position += new Vector2(1000, 2000);

// Restore the colission bits.
CollisionLayer = originalCollisionLayer;
CollisionMask = originalCollisionMask;
```

