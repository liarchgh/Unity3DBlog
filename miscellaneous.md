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

### 协程中使用协程
```
    IEnumerator Cro0()
    {
        while (True)
        {
            // Cro0等待Cro1执行完再继续执行
            yield return StartCoroutine(Cro1());
        }
    }
```

### 会产生垃圾回收

简单一个移动物体的脚本产生了125K的GC，需要注意一下  
使用```yield return null;```会好一些，因为没有返回值了

## [自定义类型转换](https://www.cnblogs.com/madkex/archive/2012/05/29/2523977.html)

### 隐式转换

节约了几个方法重载的代码量，懒得挨个写了

```
    public static implicit operator 目标类型(被转化类型 变量参数)
    {
       return 目标类型结果;
    }
```

### 显式转换

```
    public static explicit operator 目标类型(被转化类型 变量参数)
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

## Mask顺序
Mask的渲染顺序就是材质设定的渲染顺序

## 随机数

### 一个指定范围的随机整数
返回一个u到x范围内的随机整数，范围包含u不包含x
```Random.Range(u, x)```

### 对List<>随机排序
```
    new System.Random().Shuffle(aList);
```

## [使用集合初始值设定项初始化字典](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/how-to-initialize-a-dictionary-with-a-collection-initializer)

```
    Dictionary<int, StudentName> students = new Dictionary<int, string>()
    {
        { 111, "1"},
        { 112, "2"},
    };
```

## 按钮事件

### Raycast Target
Image或者Text等组件上有```Raycast Target```选项，选中的话当前物体会截留点击事件，不再向自己的下方传递。

### EventTrigger和ScrollRect冲突
现象：使用EventTrigger给ScrollRect中的Content下的元素添加点击事件会导致ScrollRect无法滚动，好像是需要点击非子物体的位置才行（没有验证）。
解决方法：自己新建了一个ButtonWithLongPress类，继承自Button，同时通过再Update()中调用IsPressed()获取是否时按下状态，自己实现长按事件，点击直接使用Button中的OnClick就好。
评价：比较勉强的一个解决方法，并不完美，只是刚好能用，复用性较差。

## 自动布局组件
### Horizontal Layout Group（水平布局）
### Vertical Layout Group（垂直布局）
### Grid Layout Group （网格布局） 

## 动态变化
使用DOTween插件，最开始我使用的协程自己实现，很麻烦，这个插件简单多了
```DOTween.To()```
