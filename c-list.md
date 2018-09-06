# C# List

## ForEach

### 带下标
一个第三方工具`Sirenix.Utilities`，里面提供了`List`的带有下表的ForEach方法
```
    using Sirenix.Utilities;
    class Example{
        List<Object> list = new List<Object>();
        list.ForEach((o, i) => { });
    }
```