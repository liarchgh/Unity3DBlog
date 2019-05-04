# 消息机制

## 自定义消息类

```csharp
public abstract class LSMsg : MessageBase
{
    public static short MsgType = 5484;
    
    private int _id;
    public int Id { get => _id; set => _id= value; }
    
    // Deserialize需要自己手动调用
    public override void Deserialize(NetworkReader reader)
    {
        _id = reader.ReadInt32();
    }

    // 发送消息时系统自动调用
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

## 注册消息

```csharp
NetworkServer.RegisterHandler(LSMoveModuleOnBuildingMsg.MsgType, (netMsg)=>
{
    LSMsg msg = new LSMsg();
    msg.Deserialize(netMsg.reader);
});
```

由服务器来注册消息

## 发送消息

```text
LSMsg _msg = new LSMsg();
connectionToServer?.Send(LSMsg.MsgType, _msg);
```

`Host`或`Client`发送消息

遇到的问题：这里`connectionToServer`有时候会运行两次，第一次为`null`，第二次才是正常的

