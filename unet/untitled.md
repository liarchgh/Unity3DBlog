# 消息机制

## 自定义消息类

```csharp
public abstract class LSMsg : MessageBase
{
    public static short MsgType = 5484;
    private int _id;
    public int Id { get => _id; set => _id= value; }
    public override void Deserialize(NetworkReader reader)
    {
        _id = reader.ReadInt32();
    }

    public override void Serialize(NetworkWriter writer)
    {
        writer.Write(_id);
    }
}
```

### `NetworkReader`常用读取方法

* ReadSingle\(\)

  读取一个float变量

* ReadVector3\(\)

  读取一个Vector3变量

