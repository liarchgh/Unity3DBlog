---
description: Description
---

# DynamicBone


## Root
``` The root of the transform hierarchy to apply physics. ```  
根物体，动作的起点


## Update Rate
``` Internal physics simulation rate. ```  
更新频率，简单来说就是所控制的柔性物体的运动更新频率，测试了一下，30才算是看着比较流畅，但是帧数过高之后因为柔性物体运动太快，开不出来柔性物体形变


## Update Mode
``` How much the bones slowed down. ```
- Normal
- Animate Physics  
用代码控制骨骼并且不受现有动画的影响
- Unscaled Time


## Damping
``` How much the force applied to return each bone to original orientation. ```  
降低柔体移动速度，可用AnimationCurve进行曲线定义  
与Damping进行乘算


## Elasticity(弹性)
``` How much bone's original orientation are preserved. ```  
柔性物体原位置保留的比例，也可理解为恢复原来形状的速度，可类比弹性形变，越接近就越慢  
与Damping进行乘算


## Stiffness
``` How much character's position change is ignored in physics simulation. ```  
使柔性物体不易形变  
与Damping进行乘算


## Inert
``` Each bone can be a sphere to collide with colliders. Radius describe sphere's size. ```  
每个节点的球体碰撞器(此碰撞器只与指定Dynamic Bone Collider物体碰撞，具体碰撞的物体之后由参数Colliders确定，只会被这些Dynamic Bone Collider影响，不能影响这些Dynamic Bone Collider)的半径  
与Damping进行乘算


## Colliders
指定具体会影响此柔性物体的Dynamic Bone Collider