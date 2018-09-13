# Animation

## 设置指定Clip的速度
```
    CharacterAnimation["Walk"].speed = 1;
```
倒放的话直接赋值为-1即可

## [Animation Event](https://liusuwanxia.github.io/unity/2017/05/31/Animation-Events)

# 注意

## 播放动画后直接关掉会出问题

之前再[OnDisable()](https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnDisable.html)中设置动画到某一帧，会造成之之后再次激活此物体之后无法播放动画。