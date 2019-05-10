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

