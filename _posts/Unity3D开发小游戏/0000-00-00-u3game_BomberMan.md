---
layout:   blog
istop:	  false
book:	  false
u3game:	  true
category: Unity3D-Game
ico:	  game
title:    【Unity3D开发小游戏】炸弹人游戏
date:     2020-08-21 21:09:00
background-image: https://img-blog.csdnimg.cn/20200318141109785.gif
tags:
- Unity3D
- Unity3D开发小游戏
---

@[toc]
## 一、前言

我们的炸弹人游戏灵感源于1983年的原始炸弹人，听起来像一个很古老的游戏，但是确实是一个很有趣的游戏。

我们将使用几个有趣的Unity功能，如刚体，Colliders 和Sprite Editor。我们还将学习如何正确地使用Unity的强大的Mecanim动画系统。

## 二、资源下载
UI资源和源代码请搜索QQ群：1040082875下载

## 三、让我们开始吧
### 版本
Unity 5.0.1f1
### 1.背景色
我们在Hierarchy面板中选择主照相机，在Inspector面板 ，改变一下Background颜色。最初的炸弹人游戏使用绿色背景颜色。#397 c00 (r=57，G=124，B=0)..我们可以用那种颜色，或者任何我们喜欢的颜色。我们还将调整大小属性，以便以后游戏看起来足够大：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173242230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 2.创建级别
**不可摧毁的块**
在我们的游戏中，我们将有几种类型的积木。首先，我们需要一个无法摧毁的街区。我们将使用如下工具创建32 x 32 px纹理：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1ib21iZXJtYW4tZ2FtZS9ibG9ja191bmRlc3Ryb3lhYmxlLnBuZw?x-oss-process=image/format,png)
好的，让我们在我们的项目区:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173320768.png)
我们可以修改块的导入设置:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173335559.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
注：Pixels Per Unit单位像素价值32这意味着32 x 32像素将适合在游戏世界的一个单位。我们将使用这个值的所有纹理，因为轰炸机将是32 x 32 Px稍后，我们希望他是一个准确的单位在游戏世界。

之后，我们把Block图片从Project拖入到Hierarchy面板中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173404956.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173449645.png)
**块物理**
现在，块只是游戏世界中的一个图像，一个纯粹的视觉效果，仅此而已。我们希望它成为物理世界的一部分，这样轰炸机就不能穿过它。我们可以通过选择Box Collider 2D：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173512230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在，街区是物理世界的一部分，就像一堵墙。

这里还有一件事要做。在我们的游戏中，我们将有两种类型的积木：可摧毁的和不可摧毁的积木。我们需要一种方法来找出某个块是否可以被摧毁。有很多方法可以这样做，比如编写脚本或使用标记。我们将保持简单，并使用Static属性用于不可销毁的事物：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173528520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
注意：我们通常使用Static属性来告诉Unity，某些游戏对象永远不会更改。通过这种方式，Unity可以对它们进行优化。而且，由于我们的不可摧毁的块永远不会改变，使其静态才对。
**可摧毁块**
好的，让我们在游戏中再加一个街区。和以前一样，我们将从画一个开始：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1ib21iZXJtYW4tZ2FtZS9ibG9ja19kZXN0cm95YWJsZS5wbmc?x-oss-process=image/format,png)
我们将使用以下方法导入设置为此：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173653212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后我们会把它再一次拖到Hierarchy，然后选择添加组件->Physics 2D->Box Collider 2D：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173733472.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**使用块创建级别**
现在我们可以使用我们的两个块来创建一个简单的级别。我们可以在Hierarchy然后选择Duplicate:

我们可以复制块的频率随我们的意愿，并将他们的位置，以创建一个简单的水平。我们只需记住将每个街区放置在圆角坐标处，就像(1, 2)而不是像(1.002, 1.9998).

以下是一个完整级别的样子：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190911173814663.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
注意：我们也将所有的区块分组成一个空的。砌块GameObject，我们可以在上面的菜单中创建GameObject游戏对象->创建空..但这是可选的，因为它只是为了保持我们的层次结构更干净一点。

### 3.炸弹人

好吧，让我们来创造我们的炸弹人角色。我们的角色将能够无所事事，向左，向右，上下移动。我们需要5个动画来使这成为可能。听起来会有很多工作要做，但像往常一样，团结会为我们处理所有复杂的事情。

**动画格式**
我们的动画不会像我们在制作3D游戏时使用的那样是“真实的”动画。我们只需要拍几张姿势不同的照片，然后循环播放，以实现动画效果。我们需要下列图片：
- 向左走 
- 向右走
- 向上走
- 向下走
- Idle停滞
 
 每一张的照片的尺寸很小，32px*32px，我们可以把所有的动画放到一张图片中，这样就可以在Unity里面进行切割了。
 
下面是本教程中用到的炸弹人图片：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317162915102.png)
将图片拖到到工程中，然后导入设置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031716303732.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**切割图片**
Sprite Mode选择Multiple模式，就可以将图片进行切割

我们可以单击Sprite Editor按钮：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163143528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
单击 Slice按钮，就会出现切片窗口，然后我们进行以下设置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163217304.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163227483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
最后，我们按下左上角的Apply按钮：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163255295.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
关闭Sprite Editor，我们可以看到我们的炸弹人图片现在有10个子图像：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163333611.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**制作动画**
好啦，我们有了这些切片，接下来就是制作动画了，让我们选择前两个切片，这是我们的WalkLeft动画，然后将它们拖入到场景中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163439434.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后我们就需要设置一个名称和位置，进行保存这个动画片段，我们将动画保存到我们的
Assets/BombermanAnimation文件夹，然后命名为WalkLeft.anim

然后按照上面的方法将：
WalkRight（切片2-3）
WalkDown（切片4-5）
WalkUp（切片6-7）
Idle（切片8-9）
动画制作完成

**清理**
然后将不用的东西删除掉，留下bomberman_0对象
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163836907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
将bomberman_0重命名为bomberman：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163928636.png)
我们需要一个动画控制器，但是我们不需要其他的控制器，让我们来删除其他4个控制器：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317163949103.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在我们有5个动画，然后还有一个动画控制器：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317164108649.png)
**动画控制器参数**
让我们双击bomberman_0控制器，然后我们就可以进入Animator：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317164206619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
这里我们看到的是控制炸弹人的动画状态机，它会自动在不同的动画之间切换，取决于我们给它传递的参数。

对我们来说，这些参数是炸弹人当前的运动方向，运动方向是2维的，下面的图片显示了可能的运动方向：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323101631964.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们的炸弹人只能走水平或垂直轴，不走对角线，那么：
- Y>0意味着WalkUp向上
- Y<0意味着WalkDown向下
- X>0意味着WalkRight向左
- X<0意味着WalkLeft向右
- X=0和Y=0意味着Idle不动

我们可以设置参数来控制，我们单击+号，添加一个INT类型的X和一个INT类型的Y：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317164707674.png)
根据X和Y的值来切换状态。

**添加状态**
现在只有向左的动画，让我们把向上向下向右不动的动画文件都拖入到animator：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317164842973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**创建过渡**
我们需要根据参数值来告诉状态机何时在这些状态间进行切换，比如X<0，就应该切换到向左状态。

显然要做的是添加一个从WalkRight、Walkup、Walkdown和Idle到WalkLeft的过渡

让我们右键单击任何状态，选择Make Transition，并将白色箭头拖到向左的状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031716511268.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后我们可以选择转换，点击有白色箭头的线段：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317165157552.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们禁用了 Can Transition To Self属性，避免动画一次又一次的重新启动的奇怪情况，然后添加Conditions前面说的X<0*

现在状态机会在X<0的时候，自动切换到向左状态。

让我们再添加一些其他状态：

- WalkUp向上Condition设置为Y>0
- WalkDown向下Condition设置为Y<0
- WalkRight向左Condition设置为X>0
- WalkLeft向右Condition设置为X<0
- Idle待机Condition设置为X=0和Y=0

*注意：这些状态都要禁用Can Transition to Self属性*

下面是我们设置好的状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031716562529.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**动画速度**
这里还有一项调整要做。让我们一次选择所有的状态，然后设置它们的速度属性0.4:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317165650755.png)
这样动画就不会播放得太快。

**关于动画**

我们的炸弹然动画状态机已经完成。
当第一次这样做时，这个过程可能看起来有点混乱，但是如果跟着教程来从图片到切片图像到动画的状态机转化，将这一切完成以后就会发现自己有多大的成就。
只要点击几下，就能让任何角色都有了动画效果

**注意：我们还没有看到动画在游戏中的转变，但我们很快就会看到。**

### 4.炸弹人物理
我们的炸弹人也应该成为物理世界的一部分。
添加物理：Add Component->Physics 2D->Circle Collider 2D
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317170010743.png)
*注意：我们选择了Circle Collider 2D因为这样可以更顺畅的移动，防止炸弹人被卡在边缘*


然后我们添加Rigidbody组件：
Add Component->Physics 2D->Rigidbody 2D，然后启动Fixed Angle属性，设置Gravity Scale为0：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317170216696.png)
*注意：所有能移动的东西都需要一个刚体*

### 5.炸弹人移动 
好的，让我们继续前进，让我们的炸弹人移动，首先将我们的炸弹人移动到左上角：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317170433780.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
新建脚本Move.cs：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317170454689.png)
双击打开脚本，删除Start函数和Update函数，添加FixedUpdate函数：

```csharp
using UnityEngine;
using System.Collections;

public class Move : MonoBehaviour {

    void FixedUpdate () {
    
    }
}
```
然后我们检测用户的输入，比如WSAD

下面我们就检测所有的水平和垂直按键输入：

```csharp
void FixedUpdate () {
    // Check Input Axes
    float h = Input.GetAxisRaw("Horizontal");
    float v = Input.GetAxisRaw("Vertical");
}
```
然后，新建一个speed变量：

```csharp
using UnityEngine;
using System.Collections;

public class Move : MonoBehaviour {
    public float speed = 6;

    void FixedUpdate () {
        // Check Input Axes
        float h = Input.GetAxisRaw("Horizontal");
        float v = Input.GetAxisRaw("Vertical");
    }
}
```
我们将使用刚体的速度属性来移动炸弹人，velocity 是运动方向乘以速度：

```csharp
void FixedUpdate () {
    // Check Input Axes, then use velocity
    float h = Input.GetAxisRaw("Horizontal");
    float v = Input.GetAxisRaw("Vertical");
    GetComponent<Rigidbody2D>().velocity = new Vector2(h, v) * speed;
}
```
然后我们将动画参数设置为当前的运动方向：

```csharp
void FixedUpdate () {
    // Check Input Axes, then use velocity
    float h = Input.GetAxisRaw("Horizontal");
    float v = Input.GetAxisRaw("Vertical");
    GetComponent<Rigidbody2D>().velocity = new Vector2(h, v) * speed;
    
    // Set Animation Parameters
    GetComponent<Animator>().SetInteger("X", (int)h);
    GetComponent<Animator>().SetInteger("Y", (int)v);
}
```
让我们保存脚本，然后点击Play，四处走走看：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317171009484.gif)
### 6.炸弹
**创造炸弹贴图**
让我们炸弹人有装炸弹的能力。首先，我们将炸弹的图片导入到项目中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317171058176.png)
导入设置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317171202341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
打开Sprite Editor，对图片进行切片：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317171222720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**炸弹动画**
将它们拖到场景中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031717124889.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后将动画文件保存到Assets/BombAnimation文件夹中，命名为Bomb.anim

设置Speed属性为0.5：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317171423771.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
下面是动画的样子，如果我们按下Play:
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031717155189.gif)
然后将Bomb_0重命名为Bomb

我们不希望炸弹一直在场景中，让我们保存场景，然后新建一个Prefabs文件夹，将Bomb对象拖入到Prefabs文件夹中，做成一个预制体：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317171718108.png)
然后就可以再Hierarchy中删除Bomb，因为我们不需要它了

**创建投弹脚本**
让我们创建一个脚本，在按空格的时候投下炸弹
新建脚本BombDrop.cs:
双击打开，删除Start函数：

```csharp
using UnityEngine;
using System.Collections;

public class BombDrop : MonoBehaviour {
    
    // Update is called once per frame
    void Update () {
    
    }
}
```
新建一个public对象变量，以便以后可以将预置文件拖到其中，然后我们需要检测是否按下的空格键，如果是，那么我们实例化炸弹预制件(换句话说，我们将它加载到游戏世界中):

```csharp
using UnityEngine;
using System.Collections;

public class BombDrop : MonoBehaviour {
    public GameObject bombPrefab;
    
    void Update () {
        if (Input.GetKeyDown(KeyCode.Space)) {
            Vector2 pos = transform.position;
            pos.x = Mathf.Round(pos.x);
            pos.y = Mathf.Round(pos.y);
            Instantiate(bombPrefab, pos, Quaternion.identity);
        }
    }
}
```
*注意：我们是首先得到炸弹人的位置，然后这个炸弹的位置是一个整数，比如(2,3)，没有(2.003,2.999)，我们可以使用Mathf.Round取整，然后使用Instantiate功能将炸弹预制体实例化到场景中，也就是生成，Quaternion.identity意思就是默认的旋转*

保存脚本，将脚本挂在到Bomberman对象上，选择Bomberman，将炸弹拖入到Bomb Prefab脚本的插槽中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317172557259.png)
如果我们按下Play，我们现在可以按空格键投掷炸弹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317172612760.gif)
**让炸弹爆炸**
到目前为止，我们的炸弹会一直存在在场景中，让我们在Prefabs文件夹中选择Bomb，然后单击添加组件->New Script，命名为DestroyAfter.cs

双击打开脚本，删除Update函数：

```csharp
using UnityEngine;
using System.Collections;

public class DestroyAfter : MonoBehaviour {

    // Use this for initialization
    void Start () {
    
    }
}
```
让我们添加一个time属性，记录炸弹爆炸所需时间。之后，我们将使用Destroy在“爆炸”之后销毁炸弹：

```csharp
using UnityEngine;
using System.Collections;

public class DestroyAfter : MonoBehaviour {
    public float time = 3;

    // Use this for initialization
    void Start () {
        Destroy(gameObject, time);
    }
}
```
然后我们点击Play会发现炸弹在3秒后消失，我们把脚本命名为DestroyAfter而不是Bomb是因为我们接下来可以再爆炸中重新使用它。

让我们添加另一个脚本加载爆炸到游戏中，一旦炸弹被摧毁，就加载炸弹预制体。
新建脚本Bomb.cs:
双击打开，删除Start和Update函数，添加OnDestroy函数：

```csharp
using UnityEngine;
using System.Collections;

public class Bomb : MonoBehaviour {

    void OnDestroy() {
        
    }
}
```
一旦炸弹被摧毁会自动调用该函数，我们将简单的使用这个函数来实例化爆炸：

```csharp
using UnityEngine;
using System.Collections;

public class Bomb : MonoBehaviour {
    // Explosion Prefab
    public GameObject explosionPrefab;

    void OnDestroy() {
        Instantiate(explosionPrefab, transform.position, Quaternion.identity);
    }
}
```
就这么简单。现在我们只需要制造爆炸预制件。

### 7.爆炸效果
我们想在炸弹周围产生爆炸效果。或者更准确地说，在炸弹的顶部、底部、左边、右边和中间。火的效果也应该是动画，给它一个美好的感觉。

我们将在动画爆炸中使用以下纹理：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317173632762.png)
导入设置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200317173645633.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
接着我们可以将其分割为96x96px网格，打开Sprite Editor：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318092051636.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们没有用32 x 32这一次，因为爆炸实际上涵盖了3个单位，水平和垂直。32x32乘以3等于96 x 96*

**创建爆炸动画**
将所有的切片图片拖入到场景中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031809214977.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
接着我们将命名为Explosion.anim的动画文件保存到ExplosionAnimation文件夹

接着我们点开Explosion.anim动画文件，将Speed改为0.15:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318092321762.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后再Hierarchy中将其他的对象删除，将explosion_0重命名为Explosion，然后拖入到我们的Prefabs文件夹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318092434534.png)
我们还希望爆炸效应在几秒钟后从游戏中消失，所以让我们选择添加组件，将Destroy After组件添加上去。我们将在2秒后摧毁它：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318092522562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：这是基于组件的开发的美妙之处。我们可以一次又一次地为各种不同的游戏对象重用脚本。*


这里还有一项调整要做。我们要确保爆炸永远不会发生在不可摧毁的石块上。相反，我们希望它被画在它们的后面，这样它就好像根本没有碰到它们。听起来很复杂的事情很简单，我们所要做的就是设置Order in Layer属性为小于0:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318092609478.png)
**引发爆炸**
让我们点开Bomb预制体，添加Bomb组件，然后将Explosion对象拖入到Bomb组件的ExplosionPrefab插槽中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031809281352.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
如果我们按下Play然后投下炸弹，然后我们就能看到我们的爆炸效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318092843242.gif)
**摧毁石块**
到目前为止，我们的爆炸只是视觉效果。现在是时候确保爆炸也摧毁它接触到的一切，当然，除了不可摧毁的区块。

有各种各样的方法可以做到这一点，和往常一样，我们将选择最简单的方法。我们将在爆炸中添加触发器，然后使用OnTriggerEnter2D函数来找出它所接触到的东西。

让我们在Prefabs文件夹中找到Explosion预制体，添加BoxCollider2D两次，我们将对两个碰撞器使用以下设置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318093038454.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
启用Is Trigger属性，确保我们只接受到碰撞信息，但是不与事物发生实际碰撞 ，我们调整了碰撞器大小，可以覆盖爆炸：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318093153203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后添加刚体：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318093204312.png)
*注意：这里我们要启动Is Kinematic运动学，这样刚体不会影响爆炸，只会确保收到碰撞信息，因为在Unity中参与碰撞的两个碰撞器至少有一个碰撞器是要有刚体的，不然无法触发*

让我们再创建一个脚本Explosion.cs，然后双击打开，不需要Start和Update函数，删除。
然后添加OnTriggerEnter2D函数：

```csharp
using UnityEngine;
using System.Collections;

public class Explosion : MonoBehaviour {

    void OnTriggerEnter2D(Collider2D co) {
        // Do Stuff...
    }
}
```
好的，我们想要摧毁它接触到的所有东西，除了那些我们做的静态的不可摧毁的块：

```csharp
using UnityEngine;
using System.Collections;

public class Explosion : MonoBehaviour {

    void OnTriggerEnter2D(Collider2D co) {
        if (!co.gameObject.isStatic)
            Destroy(co.gameObject);
    }
}
```
如果我们保存脚本并按下Play然后我们就可以用我们的炸弹摧毁东西了：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031809353842.gif)
### 8.制造怪物
**怪物纹理**
让我们在游戏中添加一个怪物，对于怪物，我们将使用以下纹理：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318093654831.png)
它包含了与我们炸弹人相同的5种状态动画：向上，向下，向左，向右和静止

导入设置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031809380580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后打开Sprite Editor，然后将其分割为32x32PX网格：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318093826384.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**怪物动画**
让我们将切片动画拖入到场景中，命名为WormAnimation.anim保存到WormAnimation文件夹中：
- worm_0, 1, 2  左
- worm_3, 4, 5  右
- worm_6, 7, 8  下
- worm_9, 10, 11  上
- worm_12, 13  静止

然后我们来看一下WormAnimation文件夹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318094150364.png)
之后就再场景中删除其他的对象，留下worm_0对象，将worm_0对象重命名为Worm


之后在WormAnimation文件夹中，双击worm_0对象，我们将创建怪物的动画状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318094311605.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
按照炸弹人动画状态机的操作步骤操作一遍就行了

### 9.怪物物理
怪物不能穿墙，让我们添加BoxCollider2D 和Rigidbody2D组件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318094411850.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 10.怪物移动
让我们让蠕虫随机移动，给一些人工智能的错觉。我们将首先将蠕虫放到一个有效的默认位置，而不是在墙内：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318094439525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
添加新脚本,Worm.cs脚本，双击打开，删除Update函数：

```csharp
using UnityEngine;
using System.Collections;

public class Worm : MonoBehaviour {

    // Use this for initialization
    void Start () {
    
    }
}
```
添加一个speed变量，以便我们可以控制怪物移动的速度：

```csharp
using UnityEngine;
using System.Collections;

public class Worm : MonoBehaviour {
    public float speed = 2;

    // Use this for initialization
    void Start () {
    
    }
}
```
我们希望将怪物移动到一个随机的方向，所以让我们添加一个randDir函数：

```csharp
Vector2 randDir() {
    // Set one component to -1/0/1 and one to 0
    int r = Random.Range(-1, 2);
    return (Random.value < 0.5) ? new Vector2(r, 0) : new Vector2(0, r);
}
```
*注意：我们randDir函数，返回一个上、向下、左、右或零的Vector 2。这是通过首先创建随机r值，即-1、0或1。移动x轴还是y轴是使用Random.value<0.5(这给了它50%的机会)来决定。*

我们还需要一个函数来了解怪物是否可以移动到某个方向。我们将使用UnifiedLinecast来实现：

```csharp
bool isValidDir(Vector2 dir) {        
    // Linecast to find out if anything is between worm and worm+dir
    Vector2 pos = transform.position;
    RaycastHit2D hit = Physics2D.Linecast(pos + dir, pos);
    return (hit.collider.gameObject == gameObject);
}
```
*注意：我们是从怪物要移动的位置到达怪物的位置发出一条射线，如果这条射线碰到了怪物自身，那么就说明没有东西阻挡，所以我们可以移动到那里。如果这条线碰到了其他什么东西，那么一定有什么东西挡住了它。*


好的，让我们再创建一个函数，它使用刚体的velocity使怪物向一个随机方向移动：

```csharp
void changeDir() {
    Vector2 dir = randDir();
    if (isValidDir(dir)) {
        GetComponent<Rigidbody2D>().velocity = dir * speed;
        GetComponent<Animator>().SetInteger("X", (int)dir.x);
        GetComponent<Animator>().SetInteger("Y", (int)dir.y);
    }
}
```
*注意：首先我们创建一个随机方向，然后检查怪物是否可以移动到该方向。如果可以，那么我们设置刚体的velocity。之后，我们还设置了动画的参数。*

最后，我们将使用InvokeRepeting函数每500毫秒左右更改当前移动方向：

```csharp
// Use this for initialization
void Start () {
    InvokeRepeating("changeDir", 0, 0.5f);
}
```

### 11.添加更多怪物
我们通过在Hierarchy选择怪物，然后复制粘贴，放到场景中的不同的几个地方

如果我们按下玩现在我们可以在炸弹人游戏中看到移动的怪物：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200318141109785.gif)
### 12.摘要
这是我们的Unity炸弹人教程。我们只是创造了一个有趣的小游戏和一个游戏框架。像往常一样，有很多有趣的改进可以做，比如:

- 只允许同时存在一定数量的炸弹
- 使炸弹人也收到炸弹的影响
- 使怪物易受炸弹影响
- 创建游戏菜单
- 为多人版本添加更多角色
- 把开关或者其他楼层放到积木后面
