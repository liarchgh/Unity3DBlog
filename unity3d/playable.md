---
description: Unity3D Playable API
---

# Playable

## Playable

### Controlling the play state of the tree

父节点状态设置为`Paused`，子节点会暂停，但是会保留原来的状态  
父节点状态设置为`Playing`，子节点会接着暂停时继续按照自己的状态执行

PS.这里和Unity的文档写的不太一样，文档中说:

> When setting the play state of a node, the state propagates to all its children, regardless of their play states. For example, if a child node is explicitly paused, setting a parent node to “playing” also sets all its child nodes to “playing.”
>
> In this example, the PlayableGraph contains a mixer that blends two animation clips. An AnimationClipPlayable wraps each animation clip and the SetPlayState\(\) method explicitly pauses the second playable. The second AnimationClipPlayable is explicitly paused, so its internal time does not advance and outputs the same value. The exact value depends on the specific time when the AnimationClipPlayable was paused.
>
> 大致意思：父节点设置状态后，会将它的状态传递给它的所有子节点

## Refs

* [Official Examples](https://docs.unity3d.com/2017.4/Documentation/Manual/Playables-Examples.html)
* [My test project on Gitlab](https://gitlab.com/liarchgl/testplayable)

