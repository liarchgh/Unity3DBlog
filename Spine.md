---
description: Spine in Unity3D
---

# Spine

# [开始步骤](http://zh.esotericsoftware.com/spine-unity#)

## [安装](http://zh.esotericsoftware.com/spine-unity#)

1. 下载和安装
   [Unity](http://unity3d.com/get-unity)
    \(PERSONAL版本是个人免费版.\)。
2. 创建一个空的Unity项目。
3. 下载最新版本的Spine运行库:
   [spine-unity.unitypackage](http://esotericsoftware.com/spine-unity-download/)
   。
4. 导入spine-unity.unitypackage\(你可以双击也可以将它拖进Unity中\)。
5. 在项目中打开
   `Examples\Getting Started`
   文件夹，然后打开并运行Unity Scene文件，您可以在scene中看到一些提示信息，还可以查看Inspector和示例脚本的内容。

> 在Unity中，**Spine-Unity**运行库可以加载、操作和渲染[Spine](http://esotericsoftware.com)骨骼动画。
>
> 在Unity中使用Spine-Unity可能跟别的插件结合使用。比如使用[2D Toolkit](http://www.unikronsoftware.com/2dtoolkit/)的图集系统，您可以在Unity中点击Edit-&gt;Preferences-&gt;Spine，然后点击Enable。
>
> 如果您不熟悉C\#编程和Unity的使用方式，我们建议您先查阅[Unity官方教程](http://unity3d.com/learn/tutorials)。然后从[Interface & Essentials](http://unity3d.com/learn/tutorials/topics/interface-essentials)和[Scripting](http://unity3d.com/cn/learn/tutorials/topics/scripting)这两个主题开始。但是Unity的Animation主题并不能直接适用于Spine-Unity，请直接学习Spine-Unity。
>
> Spine-Unity是在\([spine-csharp](http://esotericsoftware.com/git/spine-runtimes/tree/spine-csharp)\)基础上构建的。

## [示例代码](http://zh.esotericsoftware.com/spine-unity#)

导入最新版unitypackage之后，进入`Examples\Getting Started`目录。

打开并运行Unity Scene文件。 您可以在scene中看到一些提示信息，还可以查看Inspector和示例脚本的内容。

这些信息将介绍基本的姿势和角色动画。

您可以访问[Spine-Unity论坛](http://esotericsoftware.com/forum/viewforum.php?f=12)查阅更多信息。

## [将Spine资源导入你的项目](http://zh.esotericsoftware.com/spine-unity#Spine) {#Spine}

### [从Spine导出](http://zh.esotericsoftware.com/spine-unity#Spine) {#Spine}

1. 在创建骨架和动画之后，点击
   `Spine菜单`
   &gt;
   `导出`
   \(
   `CTRL`
   +
   `E`
   \)。这会打开
   **导出窗口**
   。
2. 在导出窗口的左边选择
   `JSON`
   。
3. 查看
   `创建图集`
   复选框。\(推荐初学者查看
   `非必要数据`
   ，
   `优质打印`
   \)。
   1. 在
      `创建图集`
      复选框旁边点击
      `设置`
      。然后会打开
      `纹理打包器设置`
      窗口。
   2. 在窗口的右下角可以看到
      `图集扩展名`
      标签，你应该将文本框中的
      `.atlas`
      设置为
      `.atlas.txt`
      。\(如果不这么做可能会出现一些问题，因为Unity默认不会识别以
      `.atlas`
      后缀的文件，虽然Spine-Unity可以识别这个文件。不管怎么样，设置为
      `.atlas.txt`
      将避免大部分的问题\)。
   3. 现在你可以关闭
      `纹理打包器设置`
      窗口了，点击
      `确定`
      关闭。
4. 在
   **导出窗口**
   中，选择一个输出文件夹。\(建议:创建一个空的文件夹，并且确定你可以找到它\)。
5. 点击
   `导出`
   。
6. 现在会导出三个文件:

* **.json**
  文件，它包含所有骨架信息。
* **.png**
  文件，它包含当前版本所有图片的集合。
* **.atlas.txt**
  文件，它包含打包的图集信息。
  > 对于**2D Toolkit**用户，第3步\(打包`.png`和`.atlas.txt`\)不是必须的。相反，你应该适当得在你的`SkeletonDataAsset`字段中添加一个`tk2dSpriteCollectionData`引用。然后在Unity中点击\``Edit`-&gt;`Preferences`-&gt;`Spine`面板中点击`Enable`启用对TK2D的支持。

### [导入Unity](http://zh.esotericsoftware.com/spine-unity#Unity) {#Unity}

1. 确保已经打开你的Unity项目

* 项目中应该已经有Spine-Unity运行库。

1. 在文件夹中找到刚才导出的3个文件。\(
   **json**
   , 
   **.atlas.txt**
    and 
   **.png**
   \)
2. 将3个文件\(或者包含它们的文件夹\)拖进Unity的
   **Project面板**
   。

* Spine-Unity运行库会根据这些文件自动生成必要的Unity资源。
* 然后你会看到3个新文件。
  * **\_Material**
    资源包含一个
    `着色器`
    引用和
    **.png**
    纹理。
  * **\_Atlas**
    资源包含一个
    `材质`
    引用和
    **.atlas.txt**
    。
  * **\_SkeletonData**
    资源包含一个
    **json**
    引用和
    **\_Atlas**
    资源。

1. 右键点击
   **\_SkeletonData**
   资源然后选择
   `Spine`
   `>`
   `Instantiate (SkeletonAnimation)`
   ，实例化一个Spine游戏对象。

* 可以通过查看
  `Examples\Getting Started`
  中的示例学习更多关于Spine游戏对象的知识。

> * **资源配置手册**
>    后期，你可以自己创建者3个文件。这种方式可以关注第3个步骤。
> * **替换着色器**
>    使用Spine-Unity默认的着色器\(
>   `Spine/Skeleton`
>    或者 
>   `Spine/SkeletonLit`
>   \)会使用
>   **Premultiplied Alpha**
>   的方式处理材质。这是Spine纹理打包器默认的设置。如果选择其他的着色器可能会产生意想不到的效果，你需要重新导出不使用
>   **Premultiplied Alpha**
>   的材质。您可以在
>   [Premultiply Alpha主题](http://esotericsoftware.com/forum/Premultiply-Alpha-3132)
>   中获得更多信息。
> * **纹理大小**
>    Unity默认会缩放过于庞大的图片。Spine-Unity运行库自动设置图集的最大大小为2048x2048。如果你的纹理比2048x2048还要大，这将导致图集坐标是错误的。所以请确保合理的导入设置，或者在Spine纹理打包器中减小最大页面的宽度和高度。
> * **纹理压缩伪像**
>    Unity2D项目默认将导入图片的纹理格式设置为"Sprite"，当使用
>   `Spine/Skeleton`
>   着色器时会导致伪像。为了避免伪像，请确保纹理类型设置为"Texture"。Spine-Unity在自动导入时会尝试应用这些设置，但是在这个过程中会更新你的纹理，这些设置可能会恢复。

# [更新你项目中的Spine-Unity运行库](http://zh.esotericsoftware.com/spine-unity#SpineUnity) {#SpineUnity}

一些Spine编辑器更新时会要求你更新Spine-Unity运行库，所以它会读取和解析导出Spine数据的正确性。

* 比如Unity的更新，我们总是建议您在更新之前备份整个Unity项目。
* 总是在更新Spine-Unity运行库之前与你的主程和美工一起检查。Spine-Unity运行库可以基于不同的项目需求而修改源代码。在你的项目中可能Spine-Unity运行库已经被程序修改过了。基于这种情况，当更新Spine-Unity运行库之后，还需要重新修改一遍。
* 更新Spine-Unity运行库，你有3个选择。便捷更新的方法是，在Unity中点击
  `Assets`-&gt;`Improt Package`-&gt;`Custom Package`
  的方式导入。另一种比较繁琐的方式是，你可以删除旧的版本，然后在导入新的版本。

## [便捷更新 \(.unitypackage\)](http://zh.esotericsoftware.com/spine-unity#unitypackage) {#unitypackage}

1. 下载最新版本的[spine-unity.unitypackage](http://esotericsoftware.com/spine-unity-download/)。
2. 双击或者拖动unitypackage导入你的Unity项目中。
3. 不管你怎么移动之前导入的运行库，在本次导入时，对话框都将显示哪些文件将会被更新。

> * 如果你的源文件损坏或者替换这个方式可能不能正确工作。对于这种情况，在导入unitypackage之前你可能需要先删除旧版本。
> * 许多unitypackage旧版本的spine-c\#源文件都是不一样的。你或许应该在更新时删除这些旧的spine-csharp文件夹。否则它会工作不正常。
> * 偶尔，一些文件会被删除或者合并。但是在导入unitypackage时并不会删除这些文件。你可以查看
>   [公告](http://esotericsoftware.com/forum/Noteworthy-Spine-Unity-Topics-5924)
>   。

## [手动 \(.unitypackage\)](http://zh.esotericsoftware.com/spine-unity#unitypackage) {#unitypackage}

1. 打开一个空的scene. \(为保险起见\)
2. 在你的Unity项目中删除之前的spine-unity和spine-csharp运行库。
3. 导入unitypackage

## [手动 \(zip from github\)](http://zh.esotericsoftware.com/spine-unity#zip-from-github) {#zip-from-github}

1. 打开一个空的scene. \(为保险起见\)
2. 从Github下载zip格式的
   [Spine运行库](https://github.com/EsotericSoftware/spine-runtimes)
   。
   1. 在你找得到的地方解压文件。\(你只需要
      `spine-csharp`
      和
      `spine-unity`
      \)。
3. 找到解压文件存放并且在你的项目中替换它们。

* 你需要以下这些文件夹:
  * `spine-csharp/src`
     \(在unitypackage中它叫做"spine-csharp"\)
  * `spine-unity/Assets/Gizmos`
    .
  * `spine-unity/Assets/spine-unity`
  * `spine-unity/Assets/Examples`
    \(可选\)

> * `Gizmos`
>   在Unity中是一个
>   [特殊文件](http://docs.unity3d.com/Manual/SpecialFolders.html)
>   。它只有放在assets根目录才能发挥作用。\(例如:
>   `Assets/Gizmos`
>   \)
> * `spine-csharp`
>    和 
>   `spine-unity`
>   可以放在任何文件夹内。
> * 有时候，你会复制许多文件。如果你这么做Unity会发出警告，请确保你复制以后删除旧的文件。
> * 一些文件可能已经被移除或者合并。请拷贝整个文件夹并且不要删除他们。然后查看关于这方面的
>   [公告](http://esotericsoftware.com/forum/Noteworthy-Spine-Unity-Topics-5924)
>   。

---

# [整体结构](http://zh.esotericsoftware.com/spine-unity#)

Spine-Unity是怎么组合到一起的？ Spine-Unity的功能由以下几个组件组成:

* Spine-C\#
* Spine-Unity
* ... Unity.

## [Spine-C\#](http://zh.esotericsoftware.com/spine-unity#SpineC) {#SpineC}

**spine-csharp**是Spine运行库使用C\#接口的公共核心。

你可以在Spine编辑器中看到这个公共核心包含的类型和数据结构的代码，其中包括`Skeleton`, `Bone`, `Slot`, `Skin`, `Attachment`, `Animation`。你可以在[Spine官方文档](http://esotericsoftware.com/spine-using-runtimes)中查看这些类型的描述。

它会将JSON\(`.json`\)和二进制\(在Unity中显示为`.skel.bytes`\)的骨架数据反序列化然后写进SkeletonData对象模型中。

它包含了基本的`AnimationState`实现、Spine的基础、以及直接可以使用的动画控制。\(更多内容请往下看\)

所有的类都是在`Spine`命名空间下。

**spine-csharp**可以让**Spine-Unity**, **Spine-XNA** and **Spine-MonoGame** — 这些C\#运行库共同使用的。因为Spine-C\#没有使用UnityEngine的类功能，所以其它适用.NET/mono编写的Spine运行库都可以在Spine-C\#基础上扩展。

为了保持老版Unity的Mono运行库和编译器，Spine-C\#没有使用C\#语言的最新功能。

### [有状态\(Stateful\) vs 无状态\(Stateless\)](http://zh.esotericsoftware.com/spine-unity#Stateful-vs-Stateless) {#Stateful-vs-Stateless}

Spine的核心类\(定义在spine-csharp中\)主要分为_stateful-instance_ 和 _stateless-data_这两种:

类似`Skeleton`、 `Bone`、 `Slot`、 `AnimationState`这些类都是_有状态_的对象，对它们进行修改不会影响到其它实例。你可以翻转`Skeleton`、复位`Bone`、修改`Slot`或者改变`AnimationState`的时间轴，并且它只适用于单例。

类似`SkeletonData`, `Animation`, `Attachment`, `BoneData`, `SlotData`这些类都是_无状态_的对象，设计初衷就是让他们可以被所有Skeleton实例交叉访问\(比如每个Spine GameObject可以创建一个骨架\)。通常，你不应该去改动这些无状态的对象。

经验之谈:

* 如果想得到
  _有状态_
  的对象，你可以使用
  `Skeleton`
  。\(比如:设置骨架的姿势或者替换一个槽的附件\)
* 如果想得到
  _无状态_
  的对象，你可以使用
  `SkeletonData`
  。\(比如:想要获得一些信息，例如
  `Animation`
  的持续性、
  `Event`
  、或者Setup/Bind姿势\)

这只是最简单的设计方案。如果你是一个高级用户或者你知道运行库是如何运行的，那么你可以根据项目需要去自定义一些"无状态"的对象。

你可以在[这里](http://esotericsoftware.com/spine-using-runtimes)找到更多关于Spine核心类的信息。

### [Spine-C\#和Spine-libGDX的区别](http://zh.esotericsoftware.com/spine-unity#SpineCSpinelibGDX) {#SpineCSpinelibGDX}

Spine-C\#主要使用C\#语言，而Spine-libGDX使用的是Java语言，然而因为C\#和Java语言的语法和传统都非常相似，这里主要说一下除了语言之外的区别。

在Spine-C\#中:

* Spine-C\#引用的核心库是
  [mscorlib](http://referencesource.microsoft.com/#mscorlib,namespaces)
  。它包含
  `Dictionary`
  和
  `Array`
  。
* 在C\#中方法和枚举变量使用
  **Pascal命名法**
  代替
  **camel命名法**
  。\(由于序列化兼容性的原因，一些枚举使用camel命名法\)
* 属性和自动属性代替Java中的getter和setter方法。这纯粹是语法和API的原因。在引擎中，属性会被MonoJIT编译器编译为方法，有时也会是内联的。
* 事件的定义和订阅可以使用C\#的事件和代理。

> 出于对性能的考虑，Spine-C\#在经常使用的代码里用`ExposedList(T)`替代`System.Collections.Generic.List(T)`。

## [Spine-Unity](http://zh.esotericsoftware.com/spine-unity#SpineUnity) {#SpineUnity}

Spine-Unity层是以Spine-C\#为基础的，所以它被允许工作在`UnityEngine`下，还会在Unity编辑器中使用inspectors和windows。

它包含Spine MonoBehaviours定义和资源文件，就像别的编辑器工具一样，为用户自动处理资源，其代码工具就像是[PropertyAttributes](http://docs.unity3d.com/ScriptReference/PropertyDrawer.html)。

Spine-Unity大部分的周期管理方法都依靠Spine-C\#遵循的[UnityEngine的生命周期和游戏循环](http://docs.unity3d.com/Manual/ExecutionOrder.html)。 但是它也包含主要的渲染代码\(在`.LateUpdate`中\)将Spine骨架转化为可见网格。

Spine-Unity也在编辑器和运行时管理Spine-C\#类的反序列化和实例化。

在编写脚本的时候，请注意:所有的Spine-C\#都应该在`Awake`中实例化。这意味着不能随意控制脚本执行顺序，不然不能保证当`Awake`被调用时已经实例化骨架和动画状态。

你应该在`Start`之后访问\(或缓存\)`.state`或`.skeleton`引用。请查看[Unity关于Awake的文档](http://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html).

### [SkeletonUtility和Spine-Unity Modules](http://zh.esotericsoftware.com/spine-unity#SkeletonUtilitySpineUnity-Modules) {#SkeletonUtilitySpineUnity-Modules}

Spine-Unity还包括一些可选的功能类和工作流

`SkeletonAnimator`允许用户使用Mecanim`动画控制器`控制动画。 SkeletonUtility允许`Spine.Bones`和`UnityEngine.Transform`之间进行转换。 这可以让你控制`UnityEngine.Transform`驱动`Bone`，或者让`GameObject`随着`Bone`运动。

在`spine-unity\Modules\`文件夹中还包括其它几个模块，它们都是直接可以用的，虽然都是一些简单得实现，但是只要稍加研究或修改就可以得到更高级得功能。

您可以在项目中任性得删除一些没有使用的模块，不用担心影响Spine的其他功能。注意:一些模块可能依赖其它的模块，所以在删除的时候应该一个一个得删。如果出现依赖问题，Unity会在编译之前提示警告。

# [控制动画](http://zh.esotericsoftware.com/spine-unity#)

![](http://i.imgur.com/7qOlCn8.png)

## [SkeletonAnimation](http://zh.esotericsoftware.com/spine-unity#SkeletonAnimation) {#SkeletonAnimation}

一般来说，`Spine.AnimationState` 管理时间轨道、更新骨架、队列、分层以及混合/交叉混合动画。如果你使用过"Mecanim"，`Spine.AnimationState`更简单，虽然属于不可编程类，但是它足够灵活，可以作为大部分动画的基本逻辑。

但是`Spine.AnimationState`是一个C\#类。要在Unity使用它，有一个包含`MonoBehaviour`的`Spine.AnimationState`对象叫做`SkeletonAnimation`。你可以在`SkeletonAnimation`里面找到一个叫做`state`的成员变量，它是`Spine.AnimationState`对象的引用。

`SkeletonAnimation`既管理更新时间，也生成Mesh对象，因为它是`SkeletonRenderer`的派生类。你可以把骨架数据资源实例化成"Spine GameObject"然后挂到`GameObject`上。你可以称SkeletonAnimation为Spine组件。

## [怎么使用SkeletonAnimation](http://zh.esotericsoftware.com/spine-unity#SkeletonAnimation) {#SkeletonAnimation}

### [对初学者来说](http://zh.esotericsoftware.com/spine-unity#)

最开始，可以使用`SkeletonAnimation`组件实例化一个`GameObject`。然后可以在Inspector中的找到`SkeletonAnimation`组件，然后点击Animation Name下拉框选择一个初始动画，当Scene启动时会直接运行这个动画。

可以设置Loop\(循环播放\)，也是可以调整TimeScale\(播放速度\)。那些在Inspector属性会映射到`.AnimationName`, `.loop` and `.timeScale`。

刚开始写代码的话，你可以给`skeletonAnimation.AnimationName`属性赋值动画的名字来切换动画。你也可以给`skeletonAnimation.loop`属性赋值为True，这样在游戏运行时你的动画会重复播放。

**skeletonAnimation**

.

**timeScale**

=

**1.5**

**f**

;

**skeletonAnimation**

.

**loop**

=

**true**

;

**skeletonAnimation**

.

**Animation**

**Name**

=

**"run"**

;

### [左右方向动画](http://zh.esotericsoftware.com/spine-unity#)

不比在Spine编辑对话框中设置动画的朝向\(向左、向右\)。`SkeletonAnimation`的`Skeleton`对象有FlipX\(还有FlipY\)的属性，你可以根据需要设置骨骼的水平镜像。

**// 如果你的角色已经是面向右边的，那么这样设置后就会面向左边。**

**    
**

**skeletonAnimation**

.

**skeleton**

.

**Flip**

**X**

=

**true**

;

然而，如果你的角色在设计时两边朝向的动画是不一样的，你可以使用Spine的皮肤功能，一个皮肤表示向左，而另一个向右，然后再设置一个变量根据不同的朝向切换皮肤。

**bool**

**facingLeft**

= \(

**facing**

!=

**"right"**

\);

**skeletonAnimation**

.

**skeleton**

.

**Flip**

**X**

=

**facingLeft**

;

**skeletonAnimation**

.

**skeleton**

.

**SetSkin**

\(

**facingLeft**

?

**"leftSkin"**

:

**"rightSkin"**

\);

### [一个典型的应用](http://zh.esotericsoftware.com/spine-unity#)

控制骨架的主要类是**Spine.AnimationState**。 `SkeletonAnimation`是基于`AnimationState`构建的，它的`SkeletonAnimation.state`引用就是`Spine.AnimationState`。它会在`Awake`中初始化，所以应该在`Start`或之后访问它。

`AnimationState`是Spine动画状态机的基础实现。它的底层在某种层面来说只能管理:更新、队列、分层和混合/交叉混合动画\(它不是Mecanim意义上的"State Machine"\)。

在代码中，你可以使用`AnimationState`的方法来播放动画:

**// 在Trank0中播放“stand”动画。**

**    
**

**skeletonAnimation**

.

**state**

.

**SetAnimation**

\(

**0**

, “

**stand**

”,

**false**

\);

**// 在Track0中添加一个“run”动画，当Track0的最后一个动画播放结束后循环播放“run”动画。**

**    
**

**skeletonAnimation**

.

**state**

.

**AddAnimation**

\(

**0**

, “

**run**

”,

**true**

,

**0**

**f**

\);

你可以在`SkeletonDataAsset`的Inspector中找到混合/淡入淡出选项。你可以在"Default Mix"中调整同一个Track中两个动画切换时的平滑程度。你也可以在这里添加指定动画之间的平滑过度程度。

#### [通道\(Track\)](http://zh.esotericsoftware.com/spine-unity#Track) {#Track}

Track是把动画分层，让角色在同一时间可以播放几个Spine动画。

这在任何情况下都是有用的，比如，你的角色正在跑动，但是还想在跑动的时候拿枪进行射击。

如果你在Track 0播放一个动感，然后在Track 1中播放另一个动画，这两个动画在同时播放时可以根据各自的需要去控制结束点和是否循环。

在动画播放过程中，高层级的通道会覆盖低层级的Track:越大的通道数字就拥有越高的优先级。

**// 跑步动画运行在Track 0，而射击动画运行在Track 1**

**    
**

**skeletonAnimation**

.

**state**

.

**SetAnimation**

\(

**0**

,

**"run"**

,

**true**

\);

**skeletonAnimation**

.

**state**

.

**SetAnimation**

\(

**1**

,

**"shoot"**

,

**false**

\);

#### [通道实体\(TrackEntry\)](http://zh.esotericsoftware.com/spine-unity#TrackEntry) {#TrackEntry}

调用`SetAnimation` 或者`AddAnimation`这两个方法后，它们会返回一个`TrackEntry`对象。

该对象代表一个正在播放或者排队的动画实例。它包含了动画的一些信息:已播放时间、播放速度和其它一些属性。

`TrackEntry`可以让你在`SetAnimation`和`AddAnimation`之外控制正在播放或排队动画的播放参数。

如果你不选择保留SetAnimation和AddAnimation返回的`TrackEntry`对象，你可以这样获得有效的`TrackEntry`对象。

**var**

**trackEntry**

=

**skeletonAnimation**

.

**state**

.

**GetCurrent**

\(

**myTrackNumber**

\);

**// 返回null，就表示没有动画在运行**

###### 当前时间 \(开始时间\)

你可以从动画的任意时间点开始播放。

例如，你可以在`SetAnimation`之后设置`.Time`的值，让动画从指定的`帧数`开始播放。但是要注意`.Time`的单位是秒。因为Spine的摄影表每秒30帧，所以你需要把帧转换为秒，公式是`time = (帧数/30f)`

**// 从第10帧开始播放"dance"动画**

**    
**

**var**

**trackEntry**

=

**skeletonAnimation**

.

**state**

.

**SetAnimation**

\(

**0**

,

**"dance"**

,

**false**

\);

**trackEntry**

.

**Time**

=

**10**

**f**

/

**30**

**f**

;

**// 你可以像这样更方便得设置Time，而不需要使用另一个变量去储存TrackEntry**

**    
**

**skeletonAnimation**

.

**state**

.

**SetAnimation**

\(

**0**

,

**"dance"**

,

**false**

\).

**Time**

=

**10**

**f**

/

**30**

**f**

;

> 如果你这么做事为了动画事件，请确保`lastTime`和`.Time`设置了一样的值。 如果`lastTime`为0， 在Time0和`.Time`之间的所有事件都将被捕获，并在下一个Update中增加/减少。

你也可以设置`.EndTime`改变动画的结束时间点。

###### 播放速度\(TimeScale\)

可以设置`TrackEntry.TimeScale`去改变播放速度。还可以从`SkeletonAnimation.timeScale`和`AnimationState.timeScale`中获得最后修改的播放速度。

> 你可以将timeScale设置为0来暂停播放。要知道，即使你将`timeScale = 0`来暂停骨骼的运动，但是每一帧的骨骼动画仍然存在，同时你对骨骼得任何更改都将会覆盖更新。

这个简单的方法可以帮助你理解怎么跳转到指定时间点:

**static**

**public**

**Spine**

.

**Track**

**Entry**

**JumpToTime**

\(

**Skeleton**

**Animation**

**skeletonAnimation**

,

**int**

**trackNumber**

,

**float**

**time**

,

**bool**

**skipEvents**

,

**bool**

**stop**

\) {

**if**

\(

**skeletonAnimation**

==

**null**

\)

**return**

**null**

;

**return**

**JumpToTime**

\(

**skeletonAnimation**

.

**state**

.

**GetCurrent**

\(

**trackNumber**

\),

**time**

,

**skipEvents**

,

**stop**

\);

}

**static**

**public**

**Spine**

.

**Track**

**Entry**

**JumpToTime**

\(

**Spine**

.

**Track**

**Entry**

**trackEntry**

,

**float**

**time**

,

**bool**

**skipEvents**

,

**bool**

**stop**

\) {

**if**

\(

**trackEntry**

!=

**null**

\) {

**trackEntry**

.

**time**

=

**time**

;

**if**

\(

**skipEvents**

\)

**trackEntry**

.

**lastTime**

=

**time**

;

**// 在3.0中，这也会忽略附件关键帧。**

**    
**

**if**

\(

**stop**

\)

**trackEntry**

.

**timeScale**

=

**0**

;

}

**return**

**trackEntry**

;

}

###### TrackEntry-特定事件.

你可以为特定动画实例订阅事件。更多信息可以查看[事件文档](http://esotericsoftware.com/spine-unity-events)。

## [Spine.Animation](http://zh.esotericsoftware.com/spine-unity#SpineAnimation) {#SpineAnimation}

`Spine.Animation`对象对应于Spine中的一个单独的"动画片段"。如果在Spine中跑步动画命名为"run"，你会得到一个叫做"run"的`Spine.Animation`对象。

每个`Spine.Animation`是`Timeline`对象的集合。每个`Timeline`对象是关键帧的集合，它定义了某个动画的值\(缩放、旋转、位置、颜色、网格、IK、事件、绘制顺序\)是怎么随时间改变的。每个`Timeline`都有它自己的目的:`Bone`的缩放、旋转和位置; `slot`的附件和颜色; `MeshAttachment`的自由变形\(FFD\)/网格顶点、还有骨架各个部分的_绘制顺序_和_事件_。

在Spine运行库中，使用`Animation.Apply(...)`将`Spine.Animation`应用在一个骨架上。这只能根据该骨架各个部分的`Timeline`和关键帧来设置姿势。如果`Timeline`不存在，则原动画值不会改变。如果`Timeline`存在，它会覆盖之前的值。

这个就是说，如果你使用`Spine.AnimationState`的Track机制同时播放两个动画，高通道的`Timeline`会覆盖低通道的`Timeline`，但是不会改变任何东西。

该系统允许用户组合**骨架各个部分的不同动画**，使它们相互独立得播放。

### [按照动画的帧/时间摆姿势](http://zh.esotericsoftware.com/spine-unity#)

~~如果你想按照某个动画的时间点去摆姿势，可以直接调用`Animation.Apply`。Spine-Unity运行库还有一个叫做`Skeleton.PoseWithAnimation`的扩展方法，它允许你按照动画的名字去摆姿势。~~

~~其中一个参数始终是时间。该时间使用秒作为单位。如果你想按照Spine中那样摆姿势，你需要在调用`Animation.Apply`或`Skeleton.PoseWithAnimation`之前调用`skeleton.SetToSetupPose()`。~~

无法使用

#### [动画连续性 \(pre-3.0\)](http://zh.esotericsoftware.com/spine-unity#pre30) {#pre30}

这也意味着，如果没有**自动复位逻辑**，动画在连续播放的时候不一定和Spine中保持一致。相反，播放一个动画序列会导致之后的动画会继承之前动画的值和骨骼姿势。

在3.0中，`Spine.AnimationState`可以让你选择性地使用**自动复位逻辑**句柄，或者你也可以使用原来的自由模式。

## [Animation Callbacks + Spine Events](http://zh.esotericsoftware.com/spine-unity#Animation-Callbacks-+-Spine-Events) {#Animation-Callbacks-+-Spine-Events}

**Spine.AnimationState** 指定动画回掉的格式请参照[C\# 事件](https://msdn.microsoft.com/en-us/library/awbftdfh.aspx)。你可以在里面找到一些处理动画播放的基础知识。

Spine.AnimationState 支持的事件:

* `Start`
   当动画开始播放，
* `End`
   当动画被清除或中断，
* `Complete`
   当动画完成它全部的持续时间，
* `Event`
   当检测到用户自定义的事件。

**警告:**

> 永远不要在订阅`End`的方法中调用`SetAnimation`。因为当一个动画被中断就会触发`End`，然而`SetAnimation`会打断所有现有的动画，这会引发**无限递归**\(End-&gt;Handle-&gt;SetAnimation-&gt;End-&gt;Handle-&gt;SetAnimation\)，导致Unity没有响应，直到堆栈溢出。

学习更多关于Spine事件和AnimationState回调，请查看[事件文档](http://esotericsoftware.com/spine-unity-events)。

### [高级动画控制](http://zh.esotericsoftware.com/spine-unity#)

Tracks和TrackEntry只是`Spine.AnimationState`的一部分，在Spine运行库中包括`AnimationState`是为了访问更快捷。它在大部分情况下可以增加性能。 然而，Spine-Unity和Spine-C\#即使没有`AnimationState`也可以起作用。一个例子是，`SkeletonAnimator`使用`UnityEngine.Animator`代替`Spine.AnimationState`，然后使用Mecanim去管理混合、分层和队列的数量和数据。

如果你想要用不同的方式统计你的动画，你可以根据打算如何使用它或者根据特殊情况去构建一个不一样的系统。

关于这点，研究[Spine运行库官方文档](http://esotericsoftware.com/spine-using-runtimes)会派得上用场。

# [渲染](http://zh.esotericsoftware.com/spine-unity#)

一般来说，Spine的系统利用现代3D游戏引擎的优势。它的高级功能更是如此，比如FFD\(自由变形\)和权重。

它通过框架和引擎\(3D术语\)连接; 在术语中有网格和顶点、还有纹理映射和UVs。所以每个图像部分由多个三角形组成的多边形来定义，或者一个矩形由两个三角形组成。这样的引擎用于2D图形，这是不常见的。

![](http://i.imgur.com/XMsoUww.jpg)

基本理念是这样的: 你已经做了三角形网格。这是Spine骨架/模型成型的基础。 你有纹理数据。这个来自纹理图集。 你有着色器程序或者混合指令。

你把这些东西都交给游戏引擎，它再交给GPU，最后由GPU渲染。纹理映射到网格，着色器和混合模式是渲染的基础。

![](http://i.imgur.com/URrFWUW.jpg)

Spine-Unity使用Unity的`MeshRenderer`和`MeshFilter`组件，还有材质资源进行渲染。这些组件都是Unity用来渲染3D模型的。

`SkeletonRenderer`类\(它的基类是`SkeletonAnimation`\)在它的`LateUpdate`方法中构建`Mesh`。它生成顶点数组、顶点颜色、三角形索引和UVs，然后把这些都放进一个`UnityEngine.Mesh`对象中。 `MeshFilter`再去获得`Mesh`，它将被`MeshRenderer`使用。 `MeshRenderer`会在适当的时间渲染网格，详情请见[Unity’s game loop](http://docs.unity3d.com/Manual/ExecutionOrder.html)。

`MeshFilter`和`MeshRenderer`都有[Retained Mode](https://en.wikipedia.org/wiki/Retained_mode)API\(与Immediate Mode API截然相反\); 也就是说，网格和材质对于持续可见并不需要每帧传递。这意味着，虽然`SkeletonRenderer`/`SkeletonAnimation`可以更新网格的每一帧，但是就算在运行时禁用更新\(通过禁用`SkeletonAnimation`或`SkeletonRenderer`\)也不会销毁现有的网格。

> **高级运用:骨架跳帧** 这也意味着，在网格生成后，你可以控制和跳过网格更新去实现特殊的跳帧和逐步更新行为。这可以减少不太重要游戏元素的更新， 或者实现一个看起来像逐帧的动画。

## [材质](http://zh.esotericsoftware.com/spine-unity#)

Spine-Unity也使用材质存储信息，包括纹理、着色器和必要的材质属性。该材质通过`AtlasAsset`分配。

`MeshRenderer`的材质数组是由`SkeletonRenderer`管理的，每一帧都取决于`AtlasAssets`需要用到什么。直接修改该数组并不是Unity典型的设置方法。

### [更多的材质](http://zh.esotericsoftware.com/spine-unity#)

你可能注意到在你的`MeshRenderer`中有很多材质，特别是，比你实际设置的`AtlasAsset`还要多。

如果你有一个以上的图集页是不正常的。渲染器的材质数组不能体现AtlasAsset中每一项的顺序和编号。SkeletonRenderer根据那些需要被渲染的Spine附件材质规划了一个材质数组。

如果所有附件共享一个材质，SkeletonRenderer只会把这个材质放进MeshRenderer。

如果一些附件用到了材质A和一些材质B，材质数组会根据材质的需要去排列顺序。这是基于附件绘制的顺序以及哪些附件可以在哪些材质纹理中。

如果是这样的顺序:

> Attachment 来自 A
>
> Attachment 来自 A
>
> Attachment 来自 B
>
> Attachment 来自 A

得到的材质数组是这样的:

> Material A \(第一和第二\)
>
> Material B \(第三\)
>
> Material A \(第四\)

换句话说，有更多的附件交替来自于A和B的话，就会有更多的材质进入材质数组，在材质数组中的每一项都表示需要转换的材质。

Dragon的例子可以说明这点: ![](http://i.imgur.com/2aHrOfh.png)

更多的材质在这个数组中，就表示会有更多的[draw calls](http://docs.unity3d.com/Manual/DrawCallBatching.html)，这会对相同骨架实例化产生不好的影响。如果你只有一个这样的骨架，它可能不是拖慢速度的主要原因。

学习更多关于Spine资源的排列，请看这个页面[Spine纹理打包器: 目录结构](http://esotericsoftware.com/spine-texture-packer#Folder-structure)

### [为每个实例设置材质属性](http://zh.esotericsoftware.com/spine-unity#)

同样的，改变MeshRenderer.material的值是没用的。

`Renderer.material`属性只是渲染器生成的副本，但是它会立即被SkeletonRenderer的渲染代码给覆盖。

另一方面，`Renderer.sharedMaterial`会修改原始材质。如果你使用这个材质生成更多的Spine游戏对象，对于它的修改应用会对所有的实例进行修改。

在这个例子中，Unity的[Renderer.SetPropertyBlock](http://docs.unity3d.com/ScriptReference/Renderer.SetPropertyBlock.html)是有用的方法。记住，`SkeletonRenderer`和`SkeletonAnimation`都使用`MeshRenderer`。设置MeshRenderer的MaterialPropertyBlock允许你改变渲染器的属性值。

**Material**

**Property**

**Block**

**mpb**

=

**new**

**MaterialPropertyBlock**

\(\);

**mpb**

.

**SetColor**

\(

**"\_FillColor"**

,

**Color**

.

**red**

\);

**// "\_FillColor" 是假设的着色器名字。**

**    
**

**GetComponent**

**&lt;**

**MeshRenderer**

**&gt;**

\(\).

**SetPropertyBlock**

\(

**mpb**

\);

> **优化的注意事项**
>
> * 使用Renderer.SetPropertyBlock允许具有相同材质的渲染器去处理那些由不同的MaterialPropertyBlocks改变的材质属性。
> * 当你在MaterialPropertyBlock中增加或改变一个属性值的时候，你需要调用
>   `SetPropertyBlock`
>   。但是你可以把MaterialPropertyBlock作为类的一部分，所以每当你想改变属性时，不必总是实例化一个新的
> * 如果你需要频繁设置一个属性，你可以使用静态方法:
>   `Shader.PropertyToID(string)`
>   去缓存一个整数ID，这个ID可以代替String，使MaterialPropertyBlock的Setter可以使用该ID去设置属性。

## [精灵纹理的渲染和Z轴次序](http://zh.esotericsoftware.com/spine-unity#Z) {#Z}

![](http://i.imgur.com/xqDt3Sn.jpg)

Spine一般使用阿尔法混合的方式去渲染你的Spine模型。

从Spine项目中绘制、上色和导出部件的时候，你导出PNG文件的像素编码格式是RGBA\(红色、绿色、蓝色和阿尔法值\)。在文件中，每个像素在阿尔法通道中有0-255的值，就像RGB通道一样，代表每个像素的透明度有256种层次。

这种透明与半透明在阿尔法通道中定义，展现深度/渲染顺序的经典问题。这些问题有许多不完善的解决方案，并且在我们今天的AAA游戏中也会发生一些奇怪的3D现象。

但是，在非常标准的方式中，也就是说i，像大多数2D阿尔法混合精灵渲染案例，包括Unity自己的`Sprite`/`SpriteRenderer`系统，Spine-Unity使用的渲染器，不使用3Dz-buffer和非阿尔法测试去确定哪些渲染在前，哪些渲染在后。

在一个网格中，它根据网格中三角形的顺序去渲染物体，然后绘制一个东西在另一个东西上面。该顺序是在Spine中控制槽的绘制顺序来决定的。

网格之间，Spine-Unity使用一些Unity的渲染顺序系统去确定 精灵/网格 应该谁上面。这是使用Spine-Unity标准配置的典型行为: Between meshes, Spine-Unity uses many of Unity’s render order systems to determine what sprite/mesh should be on top of which. Using the standard Spine-Unity setup, here is typical behavior for it:

* 网格数据被当作一个整体传递给Unity。
* 它使用GPU的triangle-by-triangle的方式渲染。
* 所有网格的渲染由多种因素确定顺序:
  * 摄像机的距离。\(摄像机判定
    [哪一种距离:平面还是透视](http://docs.unity3d.com/ScriptReference/Camera-transparencySortMode.html)
    .\)\)
  * 渲染器Sorting Layer/Sorting Order。\(
    [所有的UnityEngine.Renderers都有排序属性](https://unity3d.com/learn/tutorials/modules/beginner/2d/sorting-layers)
    .\)
  * 着色器的语言和队列标签\(默认为其他精灵的“透明”队列\)
  * Material.renderQueue。\(除非你设置它否则它就什么都不做。它只是覆盖shader语言的队列标签\)
  * [摄像机深度](http://docs.unity3d.com/ScriptReference/Camera-depth.html)
    . \(更多摄像机的设置.\)

在大多数情况下，你不需要也不应该去碰Material.renderQueue和着色器队列标签。

通过改变材质上的着色器，你可以选择用不同的着色器去获得不同的融合种类。怎么处理混合行为完全取决你。

### [分层和排序](http://zh.esotericsoftware.com/spine-unity#)

**Sorting Layer**和**Sorting Order**属性其实是在`SkeletonRenderer`/`SkeletonAnimation`的Inspector中，实际上它只是修改了`MeshRenderer`的[sorting layer](http://docs.unity3d.com/ScriptReference/Renderer-sortingLayerID.html) 和 [sorting order](http://docs.unity3d.com/ScriptReference/Renderer-sortingOrder.html) 属性.

尽管被隐藏在MeshRenderer的Inspector中，这些属性实际上是`MeshRenderer`serialized/stored的一部分，而不是SkeletonRenderer。

### [通过摄像头距离排序](http://zh.esotericsoftware.com/spine-unity#)

如果你保持所有的渲染器同样的分层和排序，他们会收到上述其他排序方案的影响。

如果队列标签页一样\(如果你使用相同的材质和着色器\)，那么你应该根据摄像机的距离去控制Spine游戏对象的排序。

别忘了这个[透视摄像机的排序模式](http://docs.unity3d.com/ScriptReference/Camera-transparencySortMode.html).

### [那么可以在我的Spine骨架的部分之间渲染任何东西吗？](http://zh.esotericsoftware.com/spine-unity#Spine) {#Spine}

有时候，你需要你的角色骑一辆自行车、举起一块石头或者拥抱一根柱子。对Spine而言，这意味着你要显示的东西，有些东西渲染在前面，有些东西渲染在后面。

在Unity中，网格是整体渲染的。那么你怎么知道哪个渲染在前面，哪个渲染在后面？

对于这个问题的答案是:可能将来会改变。

但是对于现在来说，你可以使用Spine-unity的SkeletonUtility方法调用"Submesh Renderers"。它会单独覆盖。

但基本上，它的作用是让你的`SkeletonRenderer`网格根据槽\(上面和下面\)去拆分。这些拆分的部分会根据他们自己的`GameObject`中的MeshRenderers去渲染。因为他们是单独渲染的，你可以分别设置他们的`Sorting Order`。

### [我已经调低了骨架的阿尔法值，为什么还会重复显示？](http://zh.esotericsoftware.com/spine-unity#)

这在任何地方都适用的实时网格渲染。当三角形被绘制时透明度就被应用了，而不是之后。

这里大概有一些解决方案，或者一些变通方案。 去玩一些你最爱的游戏吧！你可以在各种2D游戏中找到一些变通方法的例子。

## [Spine-Unity怎么决定我的Spine模型的大小?](http://zh.esotericsoftware.com/spine-unity#SpineUnitySpine) {#SpineUnitySpine}

Spine使用 1像素:1单位。意思是，如果你只是包含图像在你的骨架中，并且没有任何旋转和缩放，在Spine中该图像的1个像素就对应1个单位高和1个单位宽。

在Unity中，1单位:1米。这是Unity默认的物理值和约束\(包括2D和3D\)。对于这点，使用1像素:1单位通常不是一个好主意。反而，Unity自己的精灵默认缩放为1/100；意味着100个像素就是1个Unity的单位大小。

为了方便，当你将Spine数据带入Unity的时候，可以将缩放设置为0.01用来匹配Unity的精灵。

![](http://i.imgur.com/4YHiEUF.png)

如果你想设置骨架的基本比例的高低，你可以在Skeleton Data Asset的Inspector中改变这个值。当你的`SkeletonData`被读取时这个值是一个乘数。当`SkeletonData`被加载并且在运行的时候去改变这个值是没有用的。

如果你想在游戏中动态得改变骨架的视觉比例\(像球这种的\)，你可以设置`gameObject.transform.localScale`属性的值。

## [水平翻转 or 垂直翻转](http://zh.esotericsoftware.com/spine-unity#or) {#or}

访问`Skeleton.FlipX`和`Skeleton.FlipY`可以允许骨架的水平翻转和垂直翻转。 这通常是个好主意，这可以让骨架朝着一个方向，所以你可以在代码中控制翻转逻辑。如果没有，你可以随时增加一个额外的`bool`变量用来控制和[取消预期翻转的布尔逻辑](http://stackoverflow.com/questions/13983198/negate-a-boolean-based-on-another-boolean).

你可能已经在Unity中学会怎么反转2D精灵，设置Transform的scale为负数，或者沿着Y轴旋转180度。 这两件事纯粹是视觉的目的。但是它们有其副作用，请记住:

* 不均匀的缩放会导致一个网格绕过Unity的配料系统。这意味着每个实例都会有它自己的draw calls。所以对于你的主要角色这没什么问题。如果你的不均匀缩放骨架的规模为数十个，它就是有害的。
* 旋转会导致法线随着网格旋转。对于2D精灵的光照，这意味着它们会指向错误的方位。
* 旋转X或者Y也可能会导致Unity的2D碰撞发生不可预知的结果。
* 负比例的缩放会导致附加的物理碰撞和一些脚本逻辑发生不可预料的结果。

## Spine.Unity.SkeletonAnimation

实现Spine动画的脚本，导入Spine时自动添加

### state

类型是Spine.AnimationState，在Awake中初始化

可以使用它的方法来播放动画

```
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

## Spine.AnimationState

### Start

动画开始时调用\(循环：第一次动画开始时\)

### End

动画结束时调用\(循环：最后一次动画结束时\)

### Complete

### Dispost

### Interrupt

### Event



