---
layout:   blog
istop:	  false
book:	  false
u3game:	  true
category: Unity3D-Game
ico:	  game
title:    【Unity3D开发小游戏】太空射击游戏
date:     2020-08-21 21:09:00
background-image: https://img-blog.csdnimg.cn/20200323102734170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70
tags:
- Unity3D
- Unity3D开发小游戏
- 2020
---

@[TOC](《太空射击游戏》游戏教程)
## 一、前言
我们的太空射击游戏受到古老的街机游戏的启发
我们将利用物理等各种不同的Unity特征(包括刚体和碰撞器)、动画(Mecanim)，脚本(C#)，预制体，阴影和 Sprite Editor。

效果图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323102734170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

## 二、源码
UI资源和源代码请搜索QQ群：1040082875下载
## 三、正文

### 版本

**Unity 5.0.1f1**

### 1.相机调整
首先，我们将选择主照相机，将Background颜色改为黑色，并将Size调整为10:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911174234439.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 2.创建背景
**空间纹理**
我们的背景应该包括一个恒星的图像，滚动向下滚动，所以它似乎是在太空飞行的球员。我们首先画一个256 x 512PX空间背景在我们的绘图工具中的选择：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911174254302.png)
*注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。*

**导入设置**:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911174319158.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意:通常我们会将2D游戏的纹理类型设置为Sprite。但是使用UV贴图滚动纹理只适用于Texture，不适用于Sprite。Sprite是完美的像素，但滚动它们需要一个着色器，这对本教程来说太复杂了。*

### 3.添加Quad

好吧，让我们把背景添加到我们的游戏中。我们会选择GameObject->3D Object->Quad给我们的游戏添加一个四边形：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911175608795.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们使用Quad在2D游戏中，因为Texture (而不是Sprite)可以添加到它。*

现在我们来看一下Inspector，比例尺它的高宽比和我们的背景纹理是一样的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911181921217.png)

我们也会将它重命名为Background:
![Quad Renamed](https://img-blog.csdnimg.cn/20190911181926858.png)

并移除Mesh Collider因为我们不需要它(这是3D游戏):
![Remove Mesh Collider](https://img-blog.csdnimg.cn/20190911181933653.png)
之后，我们可以从项目区看到Background:
![Quad with Default Material](https://img-blog.csdnimg.cn/20190911181945784.png)

如果我们按下Play然后我们可以看到我们的空间背景，它仍然非常黑暗：
![Dark Background](https://img-blog.csdnimg.cn/20190911181953746.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

### 4.Unlit Shader
背景是黑暗的，因为它当前使用Standard只有当场景中有灯光时，着色器才会使事情变得明亮。
我们不会使用任何类型的灯光或阴影，所以让我们选择Unlit>Texture着色器：
![Background with Unlit Texture Shader](https://img-blog.csdnimg.cn/20190911182010634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

如果我们按下Play再一次，我们可以在不太暗的情况下看到背景恒星：
![Unlit Background ingame](https://img-blog.csdnimg.cn/20190911182039549.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

### 5.UV映射
如果我们仔细观察一下阴影的特性，我们就可以看到我们的紫外线了。Tiling和Offset在此：
![Background UV Properties](https://img-blog.csdnimg.cn/2019091118204911.png)
随意使用这些属性，看看它们如何改变背景。
Tiling会通过改变偏移量会改变纹理的位置。
如果我们设置Y偏移量对于像这样的值0.1, 0.2, 0.3等等，我们已经可以看到滚动发生了。

当然，为了达到滚动效果，我们不希望每秒手动更改偏移量60次。
我们会写一个Script处理好了。
让我们点击添加组件按钮，然后选择新脚本，命名为UVScroll.cs：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911182148294.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
让我们创建一个新的Scripts文件夹并将脚本移动到其中：
![UVScroll Script in Project Area](https://img-blog.csdnimg.cn/20190911182154598.png)

现在，我们可以双击脚本以便打开它：

```csharp
using UnityEngine;
using System.Collections;

public class UVScroll : MonoBehaviour {

    // Use this for initialization
    void Start () {

    }

    // Update is called once per frame
    void Update () {

    }
}
```

我们不需要Start或者Update函数，让我们移除它们。
修改UV映射在LateUpdate函数。
我们还将添加一个公共变量，让我们可以在检查器中修改滚动速度：

```csharp
using UnityEngine;
using System.Collections;

public class UVScroll : MonoBehaviour {
    public Vector2 speed;

    void LateUpdate() {
        GetComponent<Renderer>().material.mainTextureOffset = speed * Time.time;
    }
}
```

*注意：虽然看起来很简单，但是这里有很多事情发生在幕后。首先，我们使用了Vector2为了我们speed变量，以确保我们可以修改x(横向)和y(垂直)速度。我们使用GetComponent<Renderer>()访问renderer 组件。使用GetComponent<Renderer>().Matter确保UV偏移量不会被永久修改，就像手工修改它时的情况一样。相反，通过使用GetComponent<Renderer>().Matter统一创建材料的运行时脚本，并在游戏停止后删除它。此外，我们使用mainTextureOffset属性修改主纹理的UV偏移量。然后我们用Time.time实现滚动效果，请执行以下操作：Time.time是游戏开始后的时间。既然这段时间总是平稳地增长，我们不妨把它用于滚动。而且我们把时间乘以速度让它慢下来或者让它变快。因为我们速度变量是Vector2，在将它与之相乘后，它仍将是一个Time.Time..所以最后我们得到了一个新的Vector2将用于偏移两变化.*

让我们保存脚本，现在我们可以修改速度了。
我们将设置y速度(用于垂直滚动)以我们所希望的速度离开
x速度(水平滚动)在0
因此，它根本不水平滚动：
![UV Scroll in Inspector with Speed](https://img-blog.csdnimg.cn/20190911182227670.png)

### 6.滚动空间纹理
如果我们按下Play然后我们可以看到我们的背景向下滚动，就像我们在太空中飞行一样：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1zcGFjZS1zaG9vdGVyLWdhbWUvYmFja2dyb3VuZF9zY3JvbGxpbmcuZ2lm)

这个效果很好，但是我们会更进一步改善视差滚动，给它增加更多的深度。

### 7.视差滚动

我们将实现最简单形式的视差滚动，简单地覆盖两个背景纹理，并以不同的速度滚动他们。顶部的滚动速度总是快于底部的滚动。就像我们在太空中飞行一样，离我们很近的恒星也会飞过来。
滚动条比那些真的很远的星星走得更快。

让我们画另一个纹理，它大部分是透明的，里面有几颗白色的星星：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113236987.png)
*注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113339286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
新建一个Quad作为Background的子物体：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113401555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
将新的Quad重命名为Stars。Scale设置为(1,1,1)：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113445983.png)
*注意：我们可以将scale设置为(1, 1, 1)因为父GameObject已经有一个坐标为为(8, 16, 1)。因为这些恒星是它的子对象，它们会自动地被这个比例放大。因此，我们的恒星已经有了与恒星纹理相同的长径比。*

我们还将删除Mesh Collider：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113613799.png)
我们接着改变stars的纹理，我们将选择Unlit->Transparent因为我们大部分的纹理都是透明的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113657499.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们希望星星比背景更快地向下滚动，所以让我们选择
Add Component->Scripts->UVScroll然后设置Y速度到0.06:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113728496.png)
如果我们按下Play然后我们可以看到一些美丽的视差滚动：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323113802475.gif)
*注意：视差滚动是2D游戏开发中最令人佩服的视觉效果之一。它所需要的只是两个纹理，以不同的速度滚动。*

### 8.边界
**边界碰撞器**
我们将增加4个边框，以确保船只不能飞出它。
我们将添加四个碰撞器。然后我们将修改每个碰撞器，
使其中一个在左边，一个在右边，一个在顶部，另一个在底部：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115104776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
下面是它在场景:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115115595.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**边界脚本**
我们要确保子弹和敌舰在他们到达任何边界时立即摧毁他们。

让我们添加一个新脚本，名字叫做Border.cs,双击打开，删除Stat和Update函数，添加OnCollisionEnter2D函数，以便在与边界发生冲突时得到通知：

```csharp
using UnityEngine;
using System.Collections;

public class Border : MonoBehaviour {

    void OnCollisionEnter2D(Collision2D coll) {
        // Do Stuff..
    }
}
```
现在，每当有东西与边界相撞时，我们都想摧毁它，除非它是玩家的飞船：

```csharp
void OnCollisionEnter2D(Collision2D coll) {
    if (coll.gameObject.name != "PlayerShip")
        Destroy(coll.gameObject);
}
```
我们要做的就是保持现场整洁。现在，每当一艘船或一颗子弹到达界面外，它们就会自动被摧毁。

### 9.玩家飞船
**飞船图片**
让我们为玩家创造一艘漂亮的太空船。
我们将使用像Paint.NET这样的工具画一个32 x 32px飞船。
我们还将创建两个动画，一个空闲和一个飞行动画。(当用户按上箭头键时，会播放飞行动画).

我们需要一个96x64px图像保存我们所有的动画。第一行将保存Fly动画，第2行将保存空闲动画：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115545129.png)
注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115612311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
设置Sprite Mode为Multiple，然后点击Sprite Editor:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115641822.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们会切片图像为32x32px格网:
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032311565278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
点击Apple，然后关闭Sprite Editor
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032311571681.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 10.制作飞船动画
好的，现在我们有3片fly动画和2用于idle动画。选择前3片，然后将其从项目区拖入到场景:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115817717.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
保存到ShipAnimation文件夹，命名为fly.anim.

对于最后两个切片，我们将重复相同的过程，并将其保存为idle.anim.

如果我们按下Play然后我们就可以看到我们刚才拖到场景中的两个动画：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115900733.gif)
**清理**
在场景中删除ship_3，然后在项目中删除ship_3动画状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115941230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323115948919.png)
### 11.飞船动画状态机
让我们双击ship_0在我们的ShipAnimation文件夹，这样我们就可以看到Animator窗口：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323120039714.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们添加一个bool类型参数Flying，来判断飞船是否在飞行：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323140919452.png)
**添加idle状态**
这个fly状态已经在动画器中，所以让我们添加idle状态，只需拖动idle.anim文件从ShipAnimation文件夹进入Animator:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323141047190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后将两个状态链接起来，我们将选择fly状态，然后右键单击它，选择Make Transition然后拖动Make Transition选择idle状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/202003231411332.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
添加白色箭头，禁用Has Exit Time，然后添加切换条件Flying = false：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032314121328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们希望从fly到idle的时候，Flying是false*

之后，我们创建了另一个Make Transition从…idle到fly:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323141312650.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
点击白色箭头，设置条件为Flying=true：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323141336691.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 12.飞船移动
玩家应该能够通过按箭头键来控制飞船。但是不应该能穿过流星，敌舰或其他我们可能在太空遇到的东西。

为了使它成为物理世界的一部分，我们需要在我们的飞船上增加一个碰撞器和刚体。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323141511239.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323141518750.png)
*注意：我们将Gravity Scale设为0，因为在游戏中不存在重力。我们还启用了Fixed Angle以确保物理引擎在发生碰撞时不会试图旋转飞船。*

好了，既然飞船的无弹力都准备好了，接着就要去实现移动了，我们应该使用刚体组件的移动，我们可以使用AddForce和velocity

velocity 是运动方向 * 速度。以下图片显示了不同的运动方向：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323141736672.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们新建一个脚本Move.cs，双击打开，然后删除Stat和Update函数，添加一个speed变量：

```csharp
using UnityEngine;
using System.Collections;

public class Move : MonoBehaviour {
    // Ship Speed
    public float speed = 5;
}
```
添加FixedUpdate函数：

```csharp
using UnityEngine;
using System.Collections;

public class Move : MonoBehaviour {
    // Ship Speed
    public float speed = 5;

    void FixedUpdate() {

    }
}
```
接着就检查用户的输入，比如WSAD，或者左右上下箭头。
我们可以使用GetAxis函数，来自动检查水平和垂直轴的输入，然后返回-1 (左)和1 (右)。或0如果什么都没有按的话：

```csharp
void FixedUpdate() {
    // Get Input from Arrow Keys, WSAD, Gamepads, ...
    float h = Input.GetAxisRaw("Horizontal");
    float v = Input.GetAxisRaw("Vertical");
}
```
现在我们可以用我们的h和v值以创建dir用speed然后让它成为刚体的velocity：

```csharp
void FixedUpdate() {
    // Get Input from Arrow Keys, WSAD, Gamepads, ...
    float h = Input.GetAxisRaw("Horizontal");
    float v = Input.GetAxisRaw("Vertical");

    // Set the Rigidbody's Velocity
    Vector2 dir = new Vector2(h, v);
    GetComponent<Rigidbody2D>().velocity = dir.normalized * speed;
}
```
*注意：我们使用了normalized方向，以确保它的长度总是准确的。这是必要的，以防止船太快地移动到对角线方向(例如，当向上和右箭头键同时按下)。这个问题是基于这样一个数学事实：(1, 0)有长度1，但是向量(1, 1)实际上有长度1.41。我们还把方向乘以速度让它变得更长。这就是让飞船移动得更快的原因。*

运动本身已经完成，但我们仍然必须设置动画状态机的Flying参数，以使动画能够正确地查看。
这很容易，我们所要做的就是访问Animator组件，然后使用其SetBool函数将我们的参数设置为true或者false 
取决于垂直方向(Y)方向：

```csharp
void FixedUpdate() {
    // Get Input from Arrow Keys, WSAD, Gamepads, ...
    float h = Input.GetAxisRaw("Horizontal");
    float v = Input.GetAxisRaw("Vertical");

    // Set the Rigidbody's Velocity
    Vector2 dir = new Vector2(h, v);
    GetComponent<Rigidbody2D>().velocity = dir.normalized * speed;

    // Set Animation Parameter
    GetComponent<Animator>().SetBool("Flying", (v > 0));
}
```
*注：表达式(v>0)结果为bool值。如果v大于0它是true不然的话flase。*

如果我们按下Play然后我们可以用箭头键移动飞船：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323142735424.gif)
### 13.发射子弹
玩家应该能够用空格键发射子弹。让我们创建一个新的C#脚本来实施射击。
新建脚本FirePlayer.cs,双击打开，然后Stat函数，添加一个public的GameObject对象:

```csharp
using UnityEngine;
using System.Collections;

public class FirePlayer : MonoBehaviour {
    // Bullet Prefab
    public GameObject bullet;

    // Update is called once per frame
    void Update () {

    }
}
```
按空格生成子弹：

```csharp
using UnityEngine;
using System.Collections;

public class FirePlayer : MonoBehaviour {
    // Bullet Prefab
    public GameObject bullet;

    // Update is called once per frame
    void Update () {
        if (Input.GetKeyDown(KeyCode.Space))
            Instantiate(bullet,
                        transform.position,
                        Quaternion.identity);
    }
}
```
*注意：transform.position是当前的位置和Quaternion.identity是默认的旋转。*

我们希望确保玩家自己的子弹不会与玩家的飞船相撞：

```csharp
// Update is called once per frame
void Update () {
    if (Input.GetKeyDown(KeyCode.Space)) {
        // Spawn the Bullet
        GameObject g = (GameObject) Instantiate(bullet,
                                                transform.position,
                                                Quaternion.identity);
        // Ignore Bullet<->Player collisions
        Physics2D.IgnoreCollision(g.GetComponent<Collider2D>(),
                                  transform.parent.GetComponent<Collider2D>());
    }
}
```
*注意：使用transform.parent(在层次结构中引用GameObject的父级)以后会用到*

现在，如果我们将脚本添加到游戏中，然后按空格键，那么子弹就会被实例化在飞船的内部，这看起来很奇怪。为了防止这种情况发生，我们将创建两个BulletSpawn略高于船的位置。

让我们创建两个空对象，并且设置PlayerShip为父对象，命名为BulletSpawnLeft和BulletSpawnRight：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143312175.png)
BulletSpawnLeft设置到略高于船左翼的位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143335501.png)
BulletSpawnRight设置到略高于船右翼的位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143359902.png)
我们不能真正看到两个生成点在场景中的位置，因为它们只是空的游戏对象。你可以给他们每个人一个Gizmo然后就可以看到他们在场景中的位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143443334.png)
*注意：Gizmo只是一个视觉助手，它只显示在场景中，而不是在最后的游戏中。*

以下是与Gizmo一起出现的两个生成位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143503803.png)
然后我们给飞船添加组件FirePlayer.cs：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143533286.png)
这样就会对按空格键做出反应。我们只需要创建子弹，这样两个生成点就可以发射它。

**飞船Tag**
我们需要一种方法来确定某个游戏对象是否是一艘飞船。现在只有PlayerShip在我们的场景中，我们只需检查一下名字。但一旦有不同名称的多艘船，我们就需要一个更好的解决方案。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143631312.png)
让我们选择加上标签..。从标记列表中添加一个Ship标签：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143649927.png)
之后，我们可以选择PlayerShip然后再分配Ship贴在上面：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143712913.png)
*注意：我们可以在脚本里使用gameObject.tag*

### 14.制作子弹
**子弹纹理**
让我们创造一个子弹纹理，这样飞船就可以拍摄了。我们将使用16 x 16PX图像：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143825168.png)
*注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143840963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
拖入到场景中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323143901746.png)
### 15.子弹物理
**添加碰撞器和刚体**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032314393577.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 16.让子弹飞
接下来，我们会让子弹飞向某个方向。如果我们再想一想，玩家的子弹，敌人的子弹，以及敌人的飞船本身，在默认情况下都必须飞向某个特定的方向。因此，让我们为每个脚本创建一个脚本。

新建脚本ContinuousVelocity.cs，双击打开，删除Start函数和Update函数，添加FixedUpdate函数：

```csharp
using UnityEngine;
using System.Collections;

public class ContinuousVelocity : MonoBehaviour {
    // The Velocity
    public Vector2 velocity;

    void FixedUpdate() {
        GetComponent<Rigidbody2D>().velocity = velocity;
    }
}
```
*注：从理论上讲，只要将速度设为一次就足够了。然而，我们要为飞船与其他船只相撞的情况做准备。要保证船在碰撞后始终保持运动，唯一的办法就是一次又一次地设定速度。*

我们还将指定一个速度，使它飞得相当快：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323144211912.png)
### 17.子弹造成伤害
新建脚本BulletDamage.cs，双击打开，删除Stat和Update函数，添加OnCollisionEnter2D函数：

```csharp
using UnityEngine;
using System.Collections;

public class BulletDamage : MonoBehaviour {

    void OnCollisionEnter2D(Collision2D coll) {
        // Do Stuff...
    }
}
```
在这里，我们可以检查子弹撞上的是否是一艘船，在这种情况下，我们可以摧毁它：

```csharp
void OnCollisionEnter2D(Collision2D coll) {
    // Collided with a Ship? Then destroy it.
    if (coll.gameObject.tag == "Ship")
        Destroy(coll.gameObject);
}
```
*注意：我们将给我们所有的船贴上标签，所以我们可以在这里检查，不用担心。我们用Destroy函数从场景中删除游戏对象。*

我们不希望子弹与某物相撞后留在现场，所以让我们销毁它：

```csharp
using UnityEngine;
using System.Collections;

public class BulletDamage : MonoBehaviour {

    void OnCollisionEnter2D(Collision2D coll) {
        // Collided with a Ship? Then destroy it.
        if (coll.gameObject.tag == "Ship")
            Destroy(coll.gameObject);

        // Destroy Bullet in any case
        Destroy(gameObject);
    }
}
```

### 18.子弹预制体
我们不希望子弹一直在场景中，我们只想在玩家真正开火的时候拥有它。

创建预制体，将子弹从Hierarchy中拖到我们的项目区Prefab文件夹中的重命名为BulletPlayer:
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032314455211.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在子弹被保存在我们的项目区我们可以随时把它加载到游戏里。
让我们从Hierarchy删除子弹因为我们不需要它从一开始就在那里。

**玩家发射子弹**
创建了子弹后，我们现在可以使用BulletPlayer预制件让飞船开枪。

让我们选择PlayerShip对象的两个子对象BulletSpawn。然后拖动BulletPlayer从项目区进入FirePlayer脚本子弹插槽：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145011556.png)
如果我们按下Play然后我们可以在按空格键上发射两颗子弹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145028744.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 19.敌人的子弹
我们将为敌舰再制造一颗子弹。这一次，它将是一个黄色Sprite：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323144655384.png)
*注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。*


现在，我们可以重复我们用于红色子弹的完全相同的工作流程。然后，我们将创建一个BulletEnemy预制体并设定速度向下飞行。

最后的结果如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032314480049.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 20.敌人
**创建纹理**
让我们在游戏中加入一些敌人。我们首先画一个32 x 32 Px敌舰形象：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145053917.png)
*注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145111828.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**创建游戏对象**

现在我们可以把敌人Sprites从项目区拖入到场景来创建一个游戏对象。

**添加碰撞器和刚体**
选中敌人然后添加组件：
Circle Collider 2D
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145135357.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145147698.png)
**敌人运动**
选中敌人，然后添加组件Continuous Velocity.cs，然后设定一个较小的下行速度：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145328484.png)
**敌人Tag**
让我们把我们的敌舰分类，就像我们对待玩家的飞船一样。我们将Tag设置为Ship然后子弹就能摧毁它：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145409126.png)
**发射子弹**
就像我们对玩家飞船所做的一样，我们也会在敌人的前面设一个子弹生成点，重命名为BulletSpawn：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145529849.png)
我们将把点定位在船底。也可以指定一个Gizmo以便于识别：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145642427.png)
新建一个脚本FireEnemy.cs，双击打开，删除Update函数，添加两个公有变量，一个用于子弹预制件，一个用于射击间隔：

```csharp
using UnityEngine;
using System.Collections;

public class FireEnemy : MonoBehaviour {
    // The Bullet Prefab
    public GameObject bullet;

    // The firing Interval
    public float interval = 2;

    // Use this for initialization
    void Start () {

    }
}
```
现在我们可以用Unity的InvokeRepeting函数每隔几秒钟实例化一个新的子弹：

```csharp
using UnityEngine;
using System.Collections;

public class FireEnemy : MonoBehaviour {
    // The Bullet Prefab
    public GameObject bullet;

    // The firing Interval
    public float interval = 2;

    // Use this for initialization
    void Start () {
        // Call Fire every few seconds
        InvokeRepeating("Fire", interval, interval);
    }

    void Fire() {
        // Spawn the Bullet
        GameObject g = (GameObject)Instantiate(bullet,
                                               transform.position,
                                               Quaternion.identity);

        // Ignore Bullet<->Enemy Ship collisions
        Physics2D.IgnoreCollision(g.GetComponent<Collider2D>(),
                                  transform.parent.GetComponent<Collider2D>());
    }
}
```
保存脚本并查看Inspector，然后拖动BulletEnemy预置体到脚本中子弹插槽：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145833770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
如果我们按下Play现在我们可以看到敌舰每隔几秒钟就发射一颗子弹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145847254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
敌人不必从一开始就出现在现场，相反，我们会在稍后进行。所以让我们把它重命名为EnemyShip，然后拖入到Prefabs文件夹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323145915206.png)
让我们在Hierarchy中删除这个对象

### 21.生成敌人
让我们创建5个空游戏对象，命名为Spawner，然后设置Gizmo，我们将它们放到场景的顶端：
- (-3, 7)
- (-1.5, 7)
- (0, 7)
- (1.5, 7)
- (3, 7)

下面是它在场景:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323150122614.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
选中所有的Spawner，添加脚本Spawn.cs,双击打开：

```csharp
using UnityEngine;
using System.Collections;

public class Spawn : MonoBehaviour {

    // Use this for initialization
    void Start () {

    }

    // Update is called once per frame
    void Update () {

    }
}
```
我们已经知道如何实例化每隔几秒钟就生成一次：

```csharp
using UnityEngine;
using System.Collections;

public class Spawn : MonoBehaviour {
    // The Ship
    public GameObject ship;

    // The Interval
    public float interval = 1;

    // Use this for initialization
    void Start () {
        InvokeRepeating("SpawnNext", interval, interval);
    }

    void SpawnNext () {
        Instantiate(ship, transform.position, Quaternion.identity);
    }
}
```
保存脚本后，我们可以将EnemyShip从项目区拖入到Ship插槽：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323150242714.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后给每个Spawner设置一个不同的间隔Interval。


如果我们按下Play现在我们可以看到几艘敌舰在游戏的顶端生成：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323150335148.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在我们就可以开始太空射击游戏了：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032315035734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 22.摘要
在本教程中，我们创建了一个天空射击游戏Unity版本的框架，我们学习各种技巧完成了这件事，现在该由读者来使游戏尽可能的有趣了。

可以实施各种改进，例如：
- 爆炸
- 更多敌舰
- 菜单
- 输赢的屏幕
- 更多动画
- 高分
- 飞船升级
- 不同关卡
