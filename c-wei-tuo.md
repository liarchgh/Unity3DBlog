# C\#委托

## [使用委托（C\# 编程指南）](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/delegates/using-delegates) {#using-delegates-c-programming-guide}

[委托](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/delegate)是安全封装方法的类型，类似于 C 和 C++ 中的函数指针。 与 C 函数指针不同的是，委托是面向对象的、类型安全的和可靠的。 委托的类型由委托的名称确定。 以下示例声明名为 `Del` 的委托，该委托可以封装采用[字符串](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/string)作为参数并返回 [void](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/void) 的方法：C\#

```text
public delegate void Del(string message);
```

委托对象通常通过提供委托将封装的方法的名称或使用[匿名方法](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-methods)构造。 对委托进行实例化后，委托会将对其进行的方法调用传递到该方法。 调用方传递到委托的参数将传递到该方法，并且委托会将方法的返回值（如果有）返回到调用方。 这被称为调用委托。 实例化的委托可以按封装的方法本身进行调用。 例如:C\#

```text
// Create a method for a delegate.
public static void DelegateMethod(string message)
{
    System.Console.WriteLine(message);
}
```

C\#

```text
// Instantiate the delegate.
Del handler = DelegateMethod;

// Call the delegate.
handler("Hello World");
```

## 参考：

* [MSDN 委托（C\# 编程指南）](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/delegates/)

