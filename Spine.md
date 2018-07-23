---
description: Spine in Unity3D
---

# Spine

## Spine.Unity.SkeletonAnimation

实现Spine动画的脚本，导入Spine时自动添加

### SkeletonAnimation.state

类型是Spine.AnimationState，在Awake中初始化

可以使用它的方法来播放动画

```
// 在Trank0中播放“stand”动画。
skeletonAnimation.state.SetAnimation(0, “stand”, false);

// 在Track0中添加一个“run”动画，当Track0的最后一个动画播放结束后循环播放“run”动画。
skeletonAnimation.state.AddAnimation(0, “run”, true, 0f);
```

### SkeletonAnimation.loop

动作是否循环

### SkeletonAnimation.AnimationName

要播放的动画的名字，直接进行赋值即可控制播放什么动画，只有在赋值与正在播放动画不一致的名字（里面的字不一样，不管是不是同一字符串）才会重新播放动作  
置为空串 `skeletonAnimation.AnimationName = ""` 时，会重新播放当前动画，此属性值依然是当前动画

### SkeletonAnimation.skeleton.FlipX

控制物体水平朝向，bool类型，取反即物体水平朝向反过来
### SkeletonAnimation.timeScale

时间缩放，动作的实际速度是动作的初始速度呈上此参数

### SkeletonAnimation.state
类型：Spine.AnimationState

## Track

可以设置不同Track的动画来同时播放多个动画，高层级的通道会覆盖低层级的Track:越大的通道数字就拥有越高的优先级

```
// 跑步动画运行在Track 0，而射击动画运行在Track 1
skeletonAnimation.state.SetAnimation(0, "run", true);
skeletonAnimation.state.SetAnimation(1, "shoot", false);
```

## TrackEntry

获得有效的TrackEntry对象:

```
var trackEntry = skeletonAnimation.state.GetCurrent(myTrackNumber); // 返回null，就表示没有动画在运行
```

### TrackEntry.Time,TrackEntry.lastTime
指定帧开始播放
Spine的摄影表每秒30帧

```
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