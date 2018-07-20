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

#### Track
可以设置不同Track的动画来同时播放多个动画，高层级的通道会覆盖低层级的Track:越大的通道数字就拥有越高的优先级
```
// 跑步动画运行在Track 0，而射击动画运行在Track 1
skeletonAnimation.state.SetAnimation(0, "run", true);
skeletonAnimation.state.SetAnimation(1, "shoot", false);
```

#### TrackEntry
获得有效的TrackEntry对象:
```
var trackEntry = skeletonAnimation.state.GetCurrent(myTrackNumber); // 返回null，就表示没有动画在运行
```

### SkeletonAnimation.timeScale
时间缩放，动作的实际速度是动作的初始速度呈上此参数


### SkeletonAnimation.loop
动作是否循环


### SkeletonAnimation.AnimationName
要播放的动画的名字，直接进行赋值即可控制播放什么动画，只有在赋值与正在播放动画不一致的名字（里面的字不一样，不管是不是同一字符串）才会重新播放动作  
置为空串 ``` skeletonAnimation.AnimationName = "" ``` 时，会重新播放当前动画，此属性值依然是当前动画

### SkeletonAnimation..skeleton.FlipX
控制物体水平朝向，bool类型，取反即物体水平朝向反过来
