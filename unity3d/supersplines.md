# SuperSplines

一款Unity3D上的插件，用于在一系列顶点之间生成平滑的曲线

## Parameter

### Spline script

#### Nomal Mode

法线模式，可选：

* UseGlobalSplineNormal
* UseNodeNormal 每个点的朝向取决于点的法线方向设置
* UseNodeUpVector

### Spline Mesh script

#### Base Meshes

**Middle Mesh**

中间组成曲线的片段

#### MeshOptions

**Mesh Scale**

每段mesh在各个方向上的缩放

**High Accuracy**

勾选上之后各段之间连接上，否则的话可能重叠或者有空隙

#### Segmentation Optio

**Segment Count**

总的段数，有最大最小值限制

#### Button

**View Mesh**

查看最后生成的Mesh的信息

