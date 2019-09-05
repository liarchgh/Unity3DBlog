# 泛型

## [泛型类](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/generics/generic-classes) <a id="generic-classes-c-programming-guide"></a>

```csharp
void Swap<T>(List<T> list1, List<T> list2)
{
    //code to swap items
}
```

## [泛型方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/generics/generic-methods) <a id="generic-methods-c-programming-guide"></a>

```csharp
static void Swap<T>(ref T lhs, ref T rhs)
{
    T temp;
    temp = lhs;
    lhs = rhs;
    rhs = temp;
}
```

## Ref

* [泛型 - C\# 编程指南 \| Microsoft Docs](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/generics/)

