---
description: A UI framework in Unity3D.
---

# SUIFW

## 生命周期

```
    #region  窗体生命周期
    //窗口从隐藏到显示时调用
    public override void Display()
    {
        base.Display();
    }

    //从Freeze状态到重新显示时调用
    public override void Redisplay()
    {
        base.Redisplay();
    }

    //窗体显示在其他窗体下面
    public override void Freeze()
    {
        base.Freeze();
    }

    //页面隐藏(不在“栈”集合中)
    public override void Hiding()
    {
        base.Hiding();
    }
    #endregion
```

## `CloseUIForm();`

关闭当前窗口（调用此方法的窗口）

## `RigisterFullPathObjectEvent("Btn", p => ClickBtn());`

Btn按钮点击后调用ClickBtn\(\)方法

## `CurrentUIType.UIForms_Type = UIFormType.Normal;`

设置当前窗口类型

```text
    //UI窗体（位置）类型
    public enum UIFormType
    {
        //普通窗体
        Normal,   
        //固定窗体                              
        Fixed,
        //弹出窗体
        PopUp
    }
```

## `CurrentUIType.UIForms_ShowMode = UIFormShowMode.HideOther;`

设置当前窗口显示方式

```text
    //UI窗体的显示类型
    public enum UIFormShowMode
    {
        //普通
        Normal,
        //反向切换
        ReverseChange,
        //隐藏其他
        HideOther
    }
```

## 窗体透明度

```text
    //UI窗体透明度类型
    public enum UIFormLucenyType
    {
        //完全透明，不能穿透
        Lucency,
        //半透明，不能穿透
        Translucence,
        //低透明度，不能穿透
        ImPenetrable,
        //可以穿透
        Pentrate    
    }
```

## `UIManager.GetInstance().ShowUIForms(UIProConst.Form);`

加载指定Form窗口

## 与脚本生命周期关系

### Display
窗体开始:```Awake()``` &rarr; ```OnEnable()``` &rarr; ```Start()```

## 参考：

* [Unity UI框架SUIFW——LiuGuozhu](http://www.cnblogs.com/LiuGuozhu/tag/UnityUI%E6%A1%86%E6%9E%B6/)

* [【Unity插件】Event System – Dispatcher 事件系统插件 官方文档翻译](http://blog.xudawang.fun/2018/05/19/event-system-dispatcher-cn/), [pdf](http://blog.xudawang.fun/wp-content/uploads/2018/05/2018051901053669.pdf)




