---
description: Spine in Unity3D
---

# Spine

## Spine.Unity.SkeletonAnimation

实现Spine动画的脚本，导入Spine时自动添加

### state

类型是Spine.AnimationState，在Awake中初始化

可以使用它的方法来播放动画

```text
// 在Trank0中播放“stand”动画。
skeletonAnimation.state.SetAnimation(0, “stand”, false);

// 在Track0中添加一个“run”动画，当Track0的最后一个动画播放结束后循环播放“run”动画。
skeletonAnimation.state.AddAnimation(0, “run”, true, 0f);
```

### loop

动作是否循环

### AnimationName

要播放的动画的名字，直接进行赋值即可控制播放什么动画，只有在赋值与正在播放动画不一致的名字（里面的字不一样，不管是不是同一字符串）才会重新播放动作  
置为空串 `skeletonAnimation.AnimationName = ""` 时，会重新播放当前动画，此属性值依然是当前动画

### skeleton.FlipX

控制物体水平朝向，bool类型，取反即物体水平朝向反过来

### timeScale

时间缩放，动作的实际速度是动作的初始速度呈上此参数

## Track

可以设置不同Track的动画来同时播放多个动画，高层级的通道会覆盖低层级的Track:越大的通道数字就拥有越高的优先级

```text
// 跑步动画运行在Track 0，而射击动画运行在Track 1
skeletonAnimation.state.SetAnimation(0, "run", true);
skeletonAnimation.state.SetAnimation(1, "shoot", false);
```

## TrackEntry

获得有效的TrackEntry对象:

```text
var trackEntry = skeletonAnimation.state.GetCurrent(myTrackNumber); // 返回null，就表示没有动画在运行
```

### TrackEntry.Time,TrackEntry.lastTime

指定帧开始播放  
Spine的摄影表每秒30帧

```text
// 从第10帧开始播放"dance"动画
var trackEntry = skeletonAnimation.state.SetAnimation(0, "dance", false);
trackEntry.Time = 10f/30f;

// 你可以像这样更方便得设置Time，而不需要使用另一个变量去储存TrackEntry
skeletonAnimation.state.SetAnimation(0, "dance", false).Time = 10f/30f;

// 如果你这么做事为了动画事件，请确保lastTime和.Time设置了一样的值。 如果lastTime为0， 在Time0和.Time之间的所有事件都将被捕获，并在下一个Update中增加/减少。
```

### TrackEntry.animationEnd

动画的结束时间点，具体是指动画未缩放时的时间

### TrackEntry.TimeScale

播放速度，SkeletonAnimation.timeScale是最后修改的播放速度  
你可以将timeScale设置为0来暂停播放。要知道，即使你将timeScale = 0来暂停骨骼的运动，但是每一帧的骨骼动画仍然存在，同时你对骨骼得任何更改都将会覆盖更新。

## Spine.Animation

每个Spine.Animation是Timeline对象的集合

## Spine.AnimationState

### Start

动画开始时调用\(循环：第一次动画开始时\)

### End

动画结束时调用\(循环：最后一次动画结束时\)

### Complete

### Dispost

### Interrupt

### Event

## 材质

Spine-Unity也使用材质存储信息，包括纹理、着色器和必要的材质属性。该材质通过`AtlasAsset`分配。

`MeshRenderer`的材质数组是由`SkeletonRenderer`管理的，每一帧都取决于`AtlasAssets`需要用到什么。直接修改该数组并不是Unity典型的设置方法。

### 更多的材质

你可能注意到在你的`MeshRenderer`中有很多材质，特别是，比你实际设置的`AtlasAsset`还要多。

如果你有一个以上的图集页是不正常的。渲染器的材质数组不能体现AtlasAsset中每一项的顺序和编号。SkeletonRenderer根据那些需要被渲染的Spine附件材质规划了一个材质数组。

如果所有附件共享一个材质，SkeletonRenderer只会把这个材质放进MeshRenderer。

如果一些附件用到了材质A和一些材质B，材质数组会根据材质的需要去排列顺序。这是基于附件绘制的顺序以及哪些附件可以在哪些材质纹理中。

更多的材质，就表示会有更多的draw calls。

## 分层和排序

**Sorting Layer**和**Sorting Order**属性其实是在`SkeletonRenderer`/`SkeletonAnimation`的Inspector中，实际上它只是修改了`MeshRenderer`的[sorting layer](http://docs.unity3d.com/ScriptReference/Renderer-sortingLayerID.html) 和 [sorting order](http://docs.unity3d.com/ScriptReference/Renderer-sortingOrder.html) 属性.

尽管被隐藏在MeshRenderer的Inspector中，这些属性实际上是`MeshRenderer`serialized/stored的一部分，而不是SkeletonRenderer。

**Sorting Layer**中越下方的层渲染时在越上面，会遮盖掉**Sorting Layer**上面的层的物体，同一层物体靠距离摄像机距离判定

