---
description: A UI framework in Unity3D.
---

# SUIFW

## 生命周期

```text
    #region  窗体生命周期
    public override void Display()
    {
        base.Display();
        if (sas != null)
        {
            sas.AnimationState.SetAnimation(0, "attack", false);
            sas.AnimationState.TimeScale = 0.3f;
        }
    }

    public override void Redisplay()
    {
        base.Redisplay();
    }

    public override void Freeze()
    {
        base.Freeze();
    }

    public override void Hiding()
    {
        base.Hiding();
    }
    #endregion
```

### `Display()`

窗口从隐藏到显示时调用

### `Redisplay()`

上层的popup窗口关闭时调用

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

## 参考：

* [Unity UI框架SUIFW——LiuGuozhu](http://www.cnblogs.com/LiuGuozhu/tag/UnityUI%E6%A1%86%E6%9E%B6/)

