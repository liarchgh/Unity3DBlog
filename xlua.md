# XLUA

## 加载lua

* ### 运行lua语句
``` luaenv.DoString("print('success')"); ```

* ### 使用require运行文件中lua语句
``` luaenv.DoString("require 'LuaCode'"); ```
注意：默认只能读取名称为"*.lua.txt"的文件

* ### 自定义loader
```
luaenv.AddLoader(delegate(ref string filepath)
{
    string code = Resources.Load(filepath).ToString();
    return System.Text.Encoding.UTF8.GetBytes(code);
});
// 加载Resources文件夹中的LuaCode.lua.txt或者LuaCode.lua.xml文件
luaenv.DoString("require('LuaCode.lua')");
```

* ### 通过```LuaEnv.Global```获取一个全局基本数据类型
```string a = luaenv.Global.Get<string>("a");```



