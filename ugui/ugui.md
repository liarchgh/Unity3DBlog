# UGUI

## CanvasGroup

控制全部子物体的透明度

## Text

默认是固定高度、宽度的，如果想要根据内容自动调整话，只需要在`Text`组件所在的物体上添加`Content Size Filter`组件。

## Image

### Image Type

* **`Filled`**
  * `Fill Amount`

    图片的显示的比例

  * `Fill Method`

    显示的模式，包含圆形、水平、竖直等方式

## Canvas

### [获取点击位置](https://blog.csdn.net/liujunjie612/article/details/62891926)

```text
  // 若此脚本直接挂在Canvas上
  Vector2 pos;
  RectTransformUtility.ScreenPointToLocalPointInRectangle(this.transform as RectTransform,
                Input.mousePosition, this.GetComponent<Canvas>().worldCamera,out pos))
```

需要注意，返回的坐标是以`Canvas`的中心作为原点的

## EventSystem

UI响应各种操作所必须的，如果场景中不存在，按钮等UI组件都无法起作用

