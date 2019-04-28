# 序列化\(serialize\)

## [数据序列化到文件](http://xamclub.com/archives/761)

### 二进制方式

```text
void WriteTest()
{
    DemoClass demo = new DemoClass (100, "RCD");
    FileStream fs = new FileStream ("demo.bin", FileMode.OpenOrCreate);
    BinaryFormatter bf = new BinaryFormatter ();
    bf.Serialize (fs, demo);
    fs.Close ();
    Debug.LogError ("write done");
}

void ReadTest()
{
    FileStream fs = new FileStream("demo.bin", FileMode.Open);
    BinaryFormatter bf = new BinaryFormatter();
    DemoClass demo = bf.Deserialize(fs) as DemoClass;
    fs.Close();
    demo.Output();
}
```

二进制方法可以序列化`private`变量，不能序列化被`[NonSerialized]`修饰的变量且类需要被`[Serializable]`标识。

### XML方式

```text
void WriteTest()
{
    DemoClass demo = new DemoClass(100, "RCD");
    FileStream fs = new FileStream("demo.xml", FileMode.OpenOrCreate);
    XmlSerializer xml = new XmlSerializer(typeof(DemoClass));
    xml.Serialize(fs, demo);
    fs.Close();
    Debug.LogError("write done");
}

void ReadTest()
{
FileStream fs = new FileStream("demo.xml", FileMode.Open);
XmlSerializer bf = new XmlSerializer(typeof(DemoClass));
DemoClass demo = bf.Deserialize(fs) as DemoClass;
fs.Close();
demo.Output();
}
```

被序列化类必须用一个默认构造函数（二进制不需要，XML必须）

XML方法中类不需要`[Serializable]`标识，不能序列化私有变量，`[NonSerialized]`这个标识在该方法中无效

### 杂

Dicitonary数据结构无法直接序列化

并非所有的公有变量都是可以被序列化的。其中`const`，`static`是静态的，属于类而非对象，无法序列化。链表和字典在内存中的存储是不连续的，也无法序列化。其中`const`，`static`，`readonly`的区别可参考[这篇文章](http://www.cnblogs.com/suizhikuo/p/4739388.html)

