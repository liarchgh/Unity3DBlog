# C\# List

## ForEach

### 带下标

一个第三方工具`Sirenix.Utilities`，里面提供了`List`的带有下表的ForEach方法 不过是使用协程实现的

```text
    using Sirenix.Utilities;
    class Example{
        List<Object> list = new List<Object>();
        list.ForEach((o, i) => { });
    }
```

## 传值复制

* ToArray\(\)

```text
List<string> t = new List<string>(); //original
List<string> t2 = new List<string>(t.ToArray()); // copy of t
```

* ForEach

`list1.ForEach(i => list2.Add(i));`

* ConvertAll\(\)

```text
namespace Delegates
{
    class X
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }

    class Y
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            List<X> x = new List<X>();
            for (int i = 0; i < 100; i++)
                x.Add(new X { Id = i, Name = string.Format("x_{0}", i.ToString()) });
            // copy x to y
            List<Y> y = new List<Y>(x.ConvertAll<Y>(e => { return new Y { Id = e.Id, Name = e.Name }; }));
            Debug.Assert(x.Count == y.Count);
        }

    }
}
```

## [变为只读的](https://www.jb51.net/article/40688.htm)

使用List的AsReadOnly方法，只是类型也会变

```text
    List<int> a = new List<int> {1, 2, 3, 4, 5}; 
    IList<int> b = a.AsReadOnly();
```

## [自定义排序](https://msdn.microsoft.com/zh-cn/library/234b841s%28v=vs.110%29.aspx)

```text
    list.Sort((info0, info1) =>
    {
        return info0.CompareTo(info1);
    });
```

## [去重](https://blog.csdn.net/lishuangquan1987/article/details/76096022)

* 调用Distinct方法
  * 空参数

    如果List当中存放的是对象引用，Distinct方法不加参数的话，去重的规则是[调用到类的GetHashCode函数，如果返回的hashcode值不等，它就不会再调用Equels方法进行比较](https://www.cnblogs.com/xiashengwang/archive/2013/03/04/2942555.html)

  * 参数是IEqualityComparer泛型接口

    按照接口中定义的Equals来判重
* 两层循环判断

  可以使用Linq或传统循环

