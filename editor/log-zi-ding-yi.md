# Log自定义

## 双击后行为自定义

静态方法声明示例：`bool step(int instanceID, int line)`。使用`[UnityEditor.Callbacks.OnOpenAssetAttribute(-1)]`标注的此类型**静态方法**会在`Assets`被双击调用处理对应消息，双击Log也会调用。

属性的参数其实就是被调用的顺序，数字小到大，调用先到后。返回值表示你是否处理了asset的打开，如果返回`true`说明你已进行处理，不在调用之后的方法，`false`说明你不处理转会继续向后调用方法。

[完整脚本](https://blog.csdn.net/qq_26999509/article/details/78516237)：

{% code-tabs %}
{% code-tabs-item title="LogEditor.cs" %}
```csharp
using System.Reflection;
using UnityEditor;
using UnityEngine;

public class LogEditor 
{
    private class LogEditorConfig
    {
        public string logScriptPath = "";   //自定义日志脚本路径
        public string logTypeName = "";     //脚本type
        public int instanceID = 0;

        public LogEditorConfig(string logScriptPath, System.Type logType)
        {
            this.logScriptPath = logScriptPath;
            this.logTypeName = logType.FullName;
        }
    }

    //配置的日志
    private static LogEditorConfig[] _logEditorConfig = new LogEditorConfig[]
    {
        new LogEditorConfig("Assets/Scripts/DDebug/DDebug.cs",typeof(DDebug))
    };

    //处理从ConsoleWindow双击跳转
    [UnityEditor.Callbacks.OnOpenAssetAttribute(-1)]
    private static bool OnOpenAsset(int instanceID,int line)
    {
        for (int i = _logEditorConfig.Length - 1; i >= 0; --i)
        {
            var configTmp = _logEditorConfig[i];
            UpdateLogInstanceID(configTmp);
            if (instanceID == configTmp.instanceID)
            {
                var statckTrack = GetStackTrace();
                if (!string.IsNullOrEmpty(statckTrack))
                {
                    /*
                    举例说明：下面这段是一条ConsoleWindow的日志信息
                    Awake
                    UnityEngine.Debug:Log(Object)
                    DDebug:Log(String) (at Assets/Scripts/DDebug/DDebug.cs:13)
                    Test:Awake() (at Assets/Scripts/Test.cs:13)

                    说明：
                    1、其中第一行的"Awake":是指调用自定义打印日志函数的函数名，本例是在Test脚本中的Awake函数里调用的
                    2、第二行的"UnityEngine.Debug:Log(Object)":是指该日志最底层是通过Debug.Log函数打印出来的
                    3、第三行的"DDebug:Log(String) (at Assets/Scripts/DDebug/DDebug.cs:13)":指第二行的函数调用在DDebug.cs的13行
                    4、第四行的"Test:Awake() (at Assets/Scripts/Test.cs:13)":指Test.cs脚本的Awake函数调用了第二行的DDebug.cs的Log函数，在第13行
                     */

                    //通过以上信息，不难得出双击该日志应该打开Test.cs文件，并定位到第13行
                    //以换行分割堆栈信息
                    var fileNames = statckTrack.Split('\n');
                    //定位到调用自定义日志函数的那一行："Test:Awake() (at Assets/Scripts/Test.cs:13)"
                    var fileName = GetCurrentFullFileName(fileNames);
                    //定位到上例的行数：13
                    var fileLine = LogFileNameToFileLine(fileName);
                    //得到调用自定义日志函数的脚本："Assets/Scripts/Test.cs"
                    fileName = GetRealFileName(fileName);

                    //根据脚本名和行数，打开脚本
                    //"Assets/Scripts/Test.cs"
                    //13
                    AssetDatabase.OpenAsset(AssetDatabase.LoadAssetAtPath<UnityEngine.Object>(fileName), fileLine);
                    return true;
                }
                break;
            }
        }

        return false;
    }

    /// <summary>
    /// 反射出日志堆栈
    /// </summary>
    /// <returns></returns>
    private static string GetStackTrace()
    {
        var consoleWindowType = typeof(EditorWindow).Assembly.GetType("UnityEditor.ConsoleWindow");
        var fieldInfo = consoleWindowType.GetField("ms_ConsoleWindow", BindingFlags.Static | BindingFlags.NonPublic);
        var consoleWindowInstance = fieldInfo.GetValue(null);

        if (null != consoleWindowInstance)
        {
            if ((object)EditorWindow.focusedWindow == consoleWindowInstance)
            {
                fieldInfo = consoleWindowType.GetField("m_ActiveText", BindingFlags.Instance | BindingFlags.NonPublic);
                string activeText = fieldInfo.GetValue(consoleWindowInstance).ToString();
                return activeText;
            }
        }
        return "";
    }

    private static void UpdateLogInstanceID(LogEditorConfig config)
    {
        if (config.instanceID > 0)
        {
            return;
        }

        var assetLoadTmp = AssetDatabase.LoadAssetAtPath<UnityEngine.Object>(config.logScriptPath);
        if (null == assetLoadTmp)
        {
            throw new System.Exception("not find asset by path=" + config.logScriptPath);
        }
        config.instanceID = assetLoadTmp.GetInstanceID();
    }

    private static string GetCurrentFullFileName(string[] fileNames)
    {
        string retValue = "";
        int findIndex = -1;

        for (int i = fileNames.Length - 1; i >= 0; --i)
        {
            bool isCustomLog = false;
            for (int j = _logEditorConfig.Length - 1; j >= 0; --j)
            {
                if (fileNames[i].Contains(_logEditorConfig[j].logTypeName))
                {
                    isCustomLog = true;
                    break;
                }
            }
            if (isCustomLog)
            {
                findIndex = i;
                break;
            }
        }

        if (findIndex >= 0 && findIndex < fileNames.Length - 1)
        {
            retValue = fileNames[findIndex + 1];
        }

        return retValue;
    }

    private static string GetRealFileName(string fileName)
    {
        int indexStart = fileName.IndexOf("(at ") + "(at ".Length;
        int indexEnd = ParseFileLineStartIndex(fileName) - 1;

        fileName = fileName.Substring(indexStart, indexEnd - indexStart);
        return fileName;
    }

    private static int LogFileNameToFileLine(string fileName)
    {
        int findIndex = ParseFileLineStartIndex(fileName);
        string stringParseLine = "";
        for (int i = findIndex; i < fileName.Length; ++i)
        {
            var charCheck = fileName[i];
            if (!IsNumber(charCheck))
            {
                break;
            }
            else
            {
                stringParseLine += charCheck;
            }
        }

        return int.Parse(stringParseLine);
    }

    private static int ParseFileLineStartIndex(string fileName)
    {
        int retValue = -1;
        for (int i = fileName.Length - 1; i >= 0; --i)
        {
            var charCheck = fileName[i];
            bool isNumber = IsNumber(charCheck);
            if (isNumber)
            {
                retValue = i;
            }
            else
            {
                if (retValue != -1)
                {
                    break;
                }
            }
        }
        return retValue;
    }

    private static bool IsNumber(char c)
    {
        return c >= '0' && c <= '9';
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Refs

[Unity编辑器扩展-ConsoleWindow中的双击日志定位 - l449612236的博客 - CSDN博客](https://blog.csdn.net/l449612236/article/details/76087616)

[Unity - Scripting API: OnOpenAssetAttribute](https://docs.unity3d.com/ScriptReference/Callbacks.OnOpenAssetAttribute.html)

[Unity编辑器扩展-ConsoleWindow中的双击日志定位 - l449612236的博客 - CSDN博客](dhttps://blog.csdn.net/l449612236/article/details/76087616)

