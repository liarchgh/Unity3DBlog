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
```
    public static implicit 目标类型(被转化类型 变量参数)
    {
       return 目标类型结果;
    }
```

### 显示转换
```
    public static explicit 目标类型(被转化类型 变量参数)
    {
       return 目标类型结果;
    }
```

## 运算符重载
```
    public static OperatorTest operator + (OperatorTest o1, OperatorTest o2)  
    {
        OperatorTest o = new OperatorTest();
        o.Value = o1.Value + o2.Value;
        return o;
    }
```
