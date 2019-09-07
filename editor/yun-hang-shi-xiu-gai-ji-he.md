# Miscellaneous

## 运行时修改UI相关集合

运行时修改会造成UI绘制时的遍历出问题，遇到的有下标越界Error

### UnityEditorEventUtility.DelayAction

```text
UnityEditorEventUtility.DelayAction(() => { CustomFunction(); });
```

### EditorCoroutineRunner.StartEditorCoroutine

```csharp
private void Refresh()
{
    EditorCoroutineRunner.StartEditorCoroutine(DoRefresh());
}

private IEnumerator DoRefresh()
{
    // your code
    yield break;
}
```

## 添加自定义菜单

直接在静态方法上指定`MenuItem`特性即可

```text
[MenuItem("LS_Menu/ItemA")]
static void TestMenu()
{
    Debug.Log("Click LS Menu");
}
```

### 右击菜单

Project、Hierarchy、Inspector的右键菜单其实就是取的顶部的部分菜单

```text
// 在Project视图添加右击自定义菜单
[MenuItem("Assets/ItemA")]
static void MyTestA()
{
    Debug.Log(1);
}

// 在Hierarchy视图添加右击创建自定义物体菜单
// 添加到GameObject菜单的菜单项的优先级设置到0到49之间即可
[MenuItem("GameObject/ItemA",false,10)]
static void MyTestA(MenuCommand menuCommand)
{
    GameObject obj = new GameObject("ItemA");//创建新物体
    GameObjectUtility.SetParentAndAlign(obj, menuCommand.context as GameObject);//设置父节点为当前选中物体
    Undo.RegisterCreatedObjectUndo(obj, "Create" + obj.name);//注册到Undo系统,允许撤销
    Selection.activeObject = obj;//将新建物体设为当前选中物体
}
    

// 在Inspector视图添加某组件对应的右击自定义菜单
// 格式:[MenuItem("CONTEXT/脚本名称(组件名称)/菜单名称")]
[MenuItem("CONTEXT/Button/MyItem")]
static void MyTestA()
{
    Debug.Log(1);
}
```

#### Refs

[Unity 编辑器扩展（二）MenuItem（添加右击自定义菜单） - NCZ9\_ - CSDN博客](https://blog.csdn.net/NCZ9_/article/details/88561055)

[\[Unity\]扩展Hierachry的右键菜单 - yangrc1234 - 博客园](https://www.cnblogs.com/yangrouchuan/p/6690689.html)

