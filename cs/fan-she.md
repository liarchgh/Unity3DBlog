# 反射

## 调用internal访问修饰符修饰的接口

```csharp
var asm = System.Reflection.Assembly.GetAssembly(typeof(AnimatorOverrideController));
var type = asm.GetType("UnityEngine.AnimatorOverrideController");
var fieldInfo = type.GetField("OnOverrideControllerDirty", BindingFlags.Instance | BindingFlags.NonPublic);
var action = System.Delegate.CreateDelegate(fieldInfo.FieldType, this, "Repaint");
fieldInfo.SetValue(animatorOverrideController, action);
```

