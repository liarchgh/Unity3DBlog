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