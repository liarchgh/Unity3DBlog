---
description: Spine in Unity3D
---

# Spine
## Spine.Unity.SkeletonAnimation
实现Spine动画的脚本，导入Spine时自动添加


### SkeletonAnimation.state


### SkeletonAnimation.timeScale
时间缩放，动作的实际速度是动作的初始速度呈上此参数


### SkeletonAnimation.loop
动作是否循环


### SkeletonAnimation.AnimationName
要播放的动画的名字，直接进行赋值即可控制播放什么动画，只有在赋值与正在播放动画不一致的名字（里面的字不一样，不管是不是同一字符串）才会重新播放动作  
置为空串 ``` skeletonAnimation.AnimationName = "" ``` 时，会重新播放当前动画，此属性值依然是当前动画