# Editor脚本的奇技淫巧

## 自动定位选择Hierarchy或Project下的对象

```text
GameObject go = GameObject.Find("Directional Light");

EditorGUIUtility.PingObject(go);
Selection.activeGameObject =  go;

//也可以选择Project下的Object
//Selection.activeObject  = AssetDatabase.LoadAssetAtPath<GameObject>("Assets/Cube.prefab");
```

### Refs

[\[UnityEditor基础\]脚本自动定位选择Hierarchy或Project下的对象 - 鳄鱼泪的博客 - CSDN博客](https://blog.csdn.net/qq_33337811/article/details/78858711)

