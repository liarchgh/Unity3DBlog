Unity —生命周期

转载自:[Unity —生命周期](https://www.jianshu.com/p/8c353abb42e4)

## 一、下面我们来学习下脚本生命周期常用的10个脚本函数：

（1） Reset\(\) 组件重设为默认值时（只用于编辑状态）  
 （2）Awake\(\) 脚本组件载入时 （调用一次）  
 （3）OnEnable\(\) 是在游戏对象可以调用时调用  
 （4） Start\(\)第一个Update发生之前 （调用一次）  
 （5）FixedUpdate\(\) 固定时间调用，常用于物理相关的计算，比如对Rigidbody的操作  
 （6）Update\(\)大部分游戏行为代码被执行的地方，除了物理代码  
 （7）LateUpdate\(\) 每帧Update调用之后  
 （8）OnGUI\(\) 绘制GUI时调用  
 （9）OnDisable\(\) 当对象设置为不可用时  
 （10）OnDestroy\(\)组件销毁时调用

## 二、下面看在程序运行后的结果

##### 1、代码： {#1、代码：}

```
void
Awake
()
{
        Debug.Log(
"Awake----1"
);
    }

void
Start
()
{
        Debug.Log(
"Start----3"
);
    }

void
OnEnable
()
{
        Debug.Log(
"OnEnable----2"
);
    }


void
LateUpdate
()
{
        Debug.Log(
"LateUpdate----6"
);
    }

void
FixedUpdate
()
{
        Debug.Log(
"FixedUpdate----4"
);
    }

void
Update
()
{
        Debug.Log(
"Update----5"
);
    }


void
OnGUI
()
{
        Debug.Log(
"OnGUI----7"
);
    }

void
OnDisable
()
{
        Debug.Log(
"OnDisable----8"
);
    }

void
OnDestroy
()
{
        Debug.Log(
"OnDestroy----9"
);
    }
```

##### 2、从下图得出，不管代码顺序如何的写都是按照以下顺序执行的： {#2、从下图得出，不管代码顺序如何的写都是按照以下顺序执行的：}

Awake -&gt;OnEable-&gt; Start -&gt; -&gt; FixedUpdate-&gt; Update -&gt; LateUpdate -&gt;OnGUI -&gt; OnDisable -&gt;OnDestroy

运行结果一：

![](https://upload-images.jianshu.io/upload_images/3620170-a5eb968024d977e8.png?imageMogr2/auto-orient/strip|imageView2/2/w/700)

这是在暂停的情况下

运行结果二：

![](https://upload-images.jianshu.io/upload_images/3620170-565d05562df4e950.png?imageMogr2/auto-orient/strip|imageView2/2/w/700)

退出运行时所调用的

---

这时在运行时，去掉在Inspector场景中Cube前面的勾后，还会调用OnDisable.

![](https://upload-images.jianshu.io/upload_images/3620170-3d85fa230bd6010f.png?imageMogr2/auto-orient/strip|imageView2/2/w/700)

Paste\_Image.png

## 三、生命周期的作用：

**1.Awake：**  
 用于在游戏开始之前初始化变量或游戏状态。在脚本整个生命周期内它仅被调用一次.Awake在所有对象被初始化之后调用，所以你可以安全的与其他对象对话或用诸如GameObject.FindWithTag\(\)这样的函数搜索它们。每个游戏物体上的Awake以随机的顺序被调用。因此，你应该用Awake来设置脚本间的引用，并用Start来传递信息Awake总是在Start之前被调用。它不能用来执行协同程序。  
**2.Start**：  
 仅在Update函数第一次被调用前调用。Start在behaviour的生命周期中只被调用一次。它和Awake的不同是Start只在脚本实例被启用时调用。你可以按需调整延迟初始化代码。Awake总是在Start之前执行。这允许你协调初始化顺序。在所有脚本实例中，Start函数总是在Awake函数之后调用。  
**3.FixedUpdate**：  
 固定帧更新，在Unity导航菜单栏中，点击“Edit”–&gt;“Project Setting”–&gt;“Time”菜单项后，右侧的Inspector视图将弹出时间管理器，其中“Fixed Timestep”选项用于设置FixedUpdate\(\)的更新频率，更新频率默认为0.02s。  
**4.Update：**  
 正常帧更新，用于更新逻辑。每一帧都执行，处理Rigidbody时，需要用FixedUpdate代替Update。例如:给刚体加一个作用力时，你必须应用作用力在FixedUpdate里的固定帧，而不是Update中的帧。\(两者帧长不同\)FixedUpdate，每固定帧绘制时执行一次，和update不同的是FixedUpdate是渲染帧执行，如果你的渲染效率低下的时候FixedUpdate调用次数就会跟着下降。FixedUpdate比较适用于物理引擎的计算，因为是跟每帧渲染有关。Update就比较适合做控制。  
**5.LateUpdate**：  
 在所有Update函数调用后被调用，和fixedupdate一样都是每一帧都被调用执行，这可用于调整脚本执行顺序。例如:当物体在Update里移动时，跟随物体的相机可以在LateUpdate里实现。LateUpdate,在每帧Update执行完毕调用，他是在所有update结束后才调用，比较适合用于命令脚本的执行。官网上例子是摄像机的跟随，都是在所有update操作完才跟进摄像机，不然就有可能出现摄像机已经推进了，但是视角里还未有角色的空帧出现。  
**6.OnGUI：**  
 在渲染和处理GUI事件时调用。比如：你画一个button或label时常常用到它。这意味着OnGUI也是每帧执行一次。  
**7.Reset**：  
 在用户点击检视面板的Reset按钮或者首次添加该组件时被调用。此函数只在编辑模式下被调用。Reset最常用于在检视面板中给定一个默认值。  
**8.OnDisable**：  
 当物体被销毁时 OnDisable将被调用，并且可用于任意清理代码。脚本被卸载时，OnDisable将被调用，OnEnable在脚本被载入后调用。注意： OnDisable不能用于协同程序。  
**9.OnDestroy**：  
 当MonoBehaviour将被销毁时，这个函数被调用。OnDestroy只会在预先已经被激活的游戏物体上被调用。注意：OnDestroy也不能用于协同程序。

\*图解（Unity3D官方文档）![](https://docs.unity3d.com/uploads/Main/monobehaviour_flowchart.svg)

![](https://docs.unity3d.com/uploads/Main/monobehaviour_flowchart.svg)

##### 如若不理解，可参考一下博客： {#如若不理解，可参考一下博客：}

[http://blog.csdn.net/akof1314/article/details/39323081](https://link.jianshu.com?t=http://blog.csdn.net/akof1314/article/details/39323081)  
[http://blog.csdn.net/zhaoguanghui2012/article/details/49121103](https://link.jianshu.com?t=http://blog.csdn.net/zhaoguanghui2012/article/details/49121103)

