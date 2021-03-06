# Ugui Rich Text

## UGUI Rich Text

### b

效果：加粗  
例子：

```text
<b>Hello World</b>
Hello World
```

![](https://i.imgur.com/yB4uzp8.png) ![](https://i.imgur.com/6gAJFJW.png)

### i

效果：斜体  
例子：

```text
<i>Hello World</i>
Hello World
```

![](https://i.imgur.com/9mDnvId.png) ![](https://i.imgur.com/Li4Nkm6.png)

### size

效果：大小  
例子：

```text
<size=40>Hello World</size>
Hello World
```

![](https://i.imgur.com/BazgJ1Y.png) ![](https://i.imgur.com/TqiDkQK.png)

### color

效果：颜色  
名称对应的颜色：  
![](https://i.imgur.com/2arUvNu.png) ![](https://i.imgur.com/k55p9bg.png)

例子：

* 使用单词指定颜色

  ```text
  <color=purple>Hello World</color>
  Hello World
  ```

  ![](https://i.imgur.com/H1Tcw9v.png) ![](https://i.imgur.com/Yem7CjG.png)

* 使用RGB指定颜色

  ```text
  <color=#ff0000>Hello World</color>
  Hello World
  ```

  ![](https://i.imgur.com/97KeYtn.png) ![](https://i.imgur.com/8Rjyigq.png)

* 使用RGBA指定颜色和透明度

  ```text
  <color=#ff000055>Hello World</color>
  Hello World
  ```

  ![](https://i.imgur.com/bkERR4m.png) ![](https://i.imgur.com/DoL2JDW.png)

### material

效果：材质，适用于text mesh中 例子：`<material=1>TestTest</material>`

### 复杂一些的应用

```text
<b><i><size=600><color=#ff000088>Hello World</color>
</size></i></b>
Hello World
```

![](https://i.imgur.com/WnpsOeQ.png) ![](https://i.imgur.com/m9B5BrS.png)

## Refs

[UGUI使用富文本Rich Text - 简书](https://www.jianshu.com/p/e9efe7e6e02b)  
[Unity - Manual: Rich Text](https://docs.unity3d.com/Manual/StyledText.html)  
[【转】（八）unity4.6Ugui中文教程文档-------概要-UGUI Rich Text - 博客园](https://www.cnblogs.com/slysky/p/4301676.html)

