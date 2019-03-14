# C#Miscellaneous

## [文件系统组织的路径字符串中分隔符](https://msdn.microsoft.com/zh-cn/library/system.io.path.directoryseparatorchar\(v=vs.110\).aspx)

```C#
    Console.WriteLine("Path.AltDirectorySeparatorChar={0}", 
        Path.AltDirectorySeparatorChar);
```
## [Color类型方法参数设置默认值](https://blog.csdn.net/fanwenyuan_fwy/article/details/72514789)

只能用重载方法的形式简介设置默认值

## [遍历Enum所有枚举量](https://www.cnblogs.com/perzy/p/3521362.html)

```C#
    enum Status{}
    foreach (Status item in Enum.GetValues(typeof(Status))){}   
```
