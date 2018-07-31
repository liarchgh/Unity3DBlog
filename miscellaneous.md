# Miscellaneous

## 协程

### 一个返回值为IEnumerator的函数

```
    IEnumerator Cro()
    {
        while (True)
        {
            yield return new WaitForSeconds(1);
        }
    }
```

### 将其作为协程启动

```
    StartCoroutine(Cro());
```

### 停止指定名称的协程

```
    StopCoroutine("Cro");
```

只能停止没有参数的协程

### 停止此脚本启动的全部协程

```
    StopAllCoroutines();
```

### 会产生垃圾回收

简单一个移动物体的脚本产生了125K的GC，需要注意一下

## [自定义类型转换](https://www.cnblogs.com/madkex/archive/2012/05/29/2523977.html)

### 隐式转换

节约了几个方法重载的代码量，懒得挨个写了

```
    public static implicit 目标类型(被转化类型 变量参数)
    {
       return 目标类型结果;
    }
```

### 显式转换

```
    public static explicit 目标类型(被转化类型 变量参数)
    {
       return 目标类型结果;
    }
```

## 运算符重载

节约了几个方法重载的代码量，懒得挨个写了

```
    public static OperatorTest operator + (OperatorTest o1, OperatorTest o2)  
    {
        OperatorTest o = new OperatorTest();
        o.Value = o1.Value + o2.Value;
        return o;
    }
```

## [Lambda 表达式](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)

可以和委托结合起来

```
    delegate int del(int i);  
    static void Main(string[] args)  
    {  
        del myDelegate = x => x * x;  
        int j = myDelegate(5); //j = 25  
    }
```

### 基本形式

```
    (input-parameters) => expression
```

### 零个参数

```
() => SomeMethod()
```

### 一个参数

```
    (x) => x * x
```

只有一个输入参数时，括号是可选的

```
    x => x * x
```

### 多个参数

```
    (x, y) => x == y
```

有时，编译器难以或无法推断输入类型，可以显式指定类型

```
    (int x, string s) => s.Length > x
```

## 引用类型作为参数时不能使用ref修饰

## 修改层级关系

UI同一层越靠下越后渲
```
    go.SetSiblingIndex(index);

```

## Serializable脚本
使用```[System.Serializable]``而不是直接继承ScriptableObject的脚本放在namespace里有问题(2018.1.0f2)


