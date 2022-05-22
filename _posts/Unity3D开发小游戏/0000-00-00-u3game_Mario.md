---
layout:   blog
istop:	  false
book:	  true
u3game:	  true
category: Unity3D-Game
ico:	  game
title:    【Unity3D开发小游戏】超级马里奥
date:     2020-08-21 21:09:00
background-image: https://img-blog.csdnimg.cn/20200319163908281.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70
tags:
- Unity3D
- Unity3D开发小游戏
---

@[TOC]
## 一、前言
超级马里奥游戏于1985年为任天堂娱乐系统发布，成为有史以来最受欢迎的电子游戏之一。

当涉及到好的游戏设计时，这个游戏是一个很好的例子。在本教程中，我们将创建游戏的一个小Demo场景，并尽可能地关注核心机制。我们将使用Unity3D引擎

和往常一样，每件事都会一步地解释，并且尽可能简单，这样每个人都能理解它。

效果图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319163908281.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
## 二、源码
UI资源和源代码请搜索QQ群：1040082875下载

## 三、正文
### 版本
==Unity5.0.0f4==

### 1.Main Camera设置
现在我们可以在Hierarchy选择主照相机使用典型的蓝色背景色 (红色=107, 绿色=140, 蓝色=255)，调整大小和位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912151509687.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 2.艺术风格
为了防止版权问题，我们不能在本教程使用原超级马里奥图片。相反，我们将画我们自己的Sprites，使他们看起来像原来的游戏。

在我们开始之前，让我们创建一个新的Sprites文件夹中的项目区:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912151631824.png)
*注意： 这就是我们把Sprite放在这里的地方。这是一个花哨的游戏开发词，用来表示图像。)*

### 3.石头
**石头的图片**
我们首先画一个16x16像素石材绘图工具中的图像，如：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1zdXBlci1tYXJpby1icm9zLWdhbWUvc3RvbmUucG5n?x-oss-process=image/format,png)
*==注意：右击图像，选择另存为。并将其保存在项目的Assets/Sprites文件夹。==*

现在，我们可以在项目区然后在Inspector修改**导入设置**:
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019091215254274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注：Pixels to Unit值为16意味着16个像素的大小等于游戏世界中一个单元的大小。我们将使用这个值作为我们所有的纹理。因此，如果我们想将两个16x16Sprites放置在一起，我们可以使用以下位置(1, 0), (2, 0)诸若此类。*

为了把它添加到游戏世界中，我们可以从项目区拖入场景中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912152625134.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
让我们在Hierarchy选择这个物体，在Inspector并将其坐标改为(0, 0, 0):
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912152718940.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*==注意：我们想制作一个2D游戏，所以我们并不真正关心Z坐标。它将是0对于我们游戏中的所有对象(除了相机)。在2D游戏中我们只关心X(水平坐标)和Y(垂直坐标)。==*

**分选层Sorting Layer**
因为我们是在一个二维游戏世界，会有一些情况下，几个图像是画在对方之上，例如，当马里奥站在灌木丛前。我们总是希望灌木丛在后台，这样马里奥就会被画在前面。(否则我们就看不到他了).

让我们告诉Unity，石头总是应该在幕后。这就是分选层我们可以更改石头的排序层，如果我们查看检查器中的Sprite Renderer组件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912152749307.png)
让我们选择添加排序层.。从分选层列表，然后添加Background层，并将其移动到第一个位置，如下所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912152805653.png)
*==注意：Unity从上到下画层，因此背景中的任何内容都将位于列表的顶部。==*

现在我们可以重新选择石头并分配我们的新Background排序层：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912152832516.png)
### 4.石头的物理
现在的石头只是一个形象，而不是物理世界的一部分，马里奥将无法在上面行走。我们需要添加一个Collider2D让它成为物理世界的一部分，这意味着事物将与石头相撞，而不是跌落或穿过石头。

我们可以添加一个Collider2D通过在Inspector选择添加组件Box Collider 2D:
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019091215342937.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在石头是物理世界的一部分，就这么简单。

### 5.添加更多的石头
现在我们可以添加更多的石头到我们的场景。我们在Hierarchy中，选中单击当前的石头，然后选择复制粘贴:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912153602121.png)
我们将把新的石头放置在(x=1，y=0):
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912153753787.png)
让我们重复这个工作流程
直到我们有两排21块石头(y=0处一行，y=-1处一列)
重要的是始终将它们放置在整数坐标上，如(2, 0)，从来没有(2.003, 0.005)
我们按下Play:
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019091215380931.png)

### 6.灌木丛和云
就像在原来的超级马里奥游戏，我们也将添加一些灌木丛和云的背景。与往常一样，我们将从绘制图像开始：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1zdXBlci1tYXJpby1icm9zLWdhbWUvY2xvdWQucG5n?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1zdXBlci1tYXJpby1icm9zLWdhbWUvY2xvdWRzLnBuZw?x-oss-process=image/format,png)
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1zdXBlci1tYXJpby1icm9zLWdhbWUvYnVzaC5wbmc?x-oss-process=image/format,png)
*==注意：右击每个图像，选择另存为.。把它们全部保存在项目中Assets/Sprites文件夹。==*

对于所有图像我们将使用以下方法**导入设置**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912153943862.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在我们可以把Sprites 从项目区拖入到场景中，把他们安置在我们想让他们去的地方：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912154015384.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
因为它们是背景的一部分，所以我们在Hierarchy中将Sorting Layer设置为Background：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912154035759.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：如前所述，背景排序层确保这些对象总是绘制在其他所有内容的后面。换句话说，马里奥总是会被绘制到他们前面。*

慢慢开始看起来像一个超级马里奥游戏了！

### 7.管道
**图片**
这些绿色管道是超级马里奥游戏的重要组成部分，所以让我们画一个：
![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9ub29idHV0cy5jb20vY29udGVudC91bml0eS8yZC1zdXBlci1tYXJpby1icm9zLWdhbWUvcGlwZS5wbmc?x-oss-process=image/format,png)
*==注意：右击图像，选择但另存为.。并将其保存在项目的Assets/Sprites文件夹。==*

下面是**导入设置**我们的管道：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912155328231.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：即使它是一个32x32像素的Sprites，我们仍然使用相同的像素值。*

现在我们可以把Sprites从我们的项目区拖入到场景
我们将在世界的右侧增加两条管道：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912155358785.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 8.管道物理
**添加碰撞器：**![在这里插入图片描述](https://img-blog.csdnimg.cn/20190912155515448.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们可以看到，管道的下部比我们的碰撞器要窄一些：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319165311580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
这没什么大不了的，让我们来用一个巧妙的小技巧来创造一个完美的碰撞器。

一种选择是只使用Polygon Collider，这会带来效率影响。

更优雅的解决方案视将另一个Collider添加到我们的管道中
然后对齐
第一个Collider使其适合管道的上部
第二个Collider使其适合管道的下部：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019091216205562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在管道的物理是完全真实的。像这样的小调整才能让游戏感觉更真实。

### 9.婴儿马里奥
**图片**
好了，现在是时候进入我们游戏中最有趣的部分了：主角。让我们画一个有点像马里奥的角色(但不太像他，出于版权原因)。
可以随意画任何你喜欢的东西，比如某种婴儿马里奥：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319165632124.png)
我们需要三个婴儿马里奥动画：
- 闲散
- 跑
- 跳

*注意：动画将由几个切片组成。如果我们在一个循环中播放几个切片，那么我们就会有一个动画。*

因此，让我们画一个包含所有动画的图像：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319165716318.png)
*注意：右键另存为，保存到Assets/Sprites文件夹*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319165747183.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

**切片图像**
我们的图像实际上是由几个小片组成的动画。
Sprite Mode设置为Multiple
单击Sprite Editor按钮：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319165838313.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后我们会选择Slice并将类型设置为Grid，然后按下Slice按钮：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319165917398.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
之后我们点击Apply，并关闭 Slice Editor 

Unity将我们的婴儿马里奥图像分割成几个16x16像素的图像，我们现在可以在项目区看到它们：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170030956.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 10.婴儿马里奥动画
好的，现在我们有了动画切片，我们可以从它们创建我们的3幅动画。作为提醒，下面是我们需要的动画：

- 闲散(第1及2段)
- 跑(第3、4及5段)
- 跳(第6及7段)

让我们创建闲散动画。我们将首先在项目区中选择切片1和2:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170125632.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后将它们拖到场景:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170221589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
将动画保存到BabyMarioAnimation文件夹，命名为Idle.anim：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170301564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
第一个文件是动画状态机，它指定诸如动画速度和状态树之类的内容。第二个是动画本身。

我们将在其余的动画中重复这个过程。(第3、4和5段命名为Run；第6和第7部分命名为Jump).

我们再Hierarchy可以看到：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170404318.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**删除不需要的**
Unity为每个动画创建了一个游戏对象，但我们只需要babymario_0，让我们选择其他的，然后删除它们：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170453751.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
在项目区，删除其他的状态机文件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170533413.png)
删除babymario_2和babymario_5：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020031917055654.png)
### 11.婴儿马里奥动画状态机
现在我们有3个动画文件，但还不知道什么时候播放哪个动画。我们需要一个动画状态机，它有三种状态：
- Idel
- Run
- Jump

我们还将添加Transitions让Unity知道什么时候该从一种动画状态切换到另一种动画状态。

让我们在BabyMarioAnimation 文件夹双击babymario_0的动画状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170758468.png)
现在我们可以看到状态机在Animator：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170826758.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
如前所述，我们需要三个状态。让我们在BabyMarioAnimation文件夹中选择Run并将其拖到此处：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319170941416.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们还将拖动jump动画进入动画：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171003781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
状态机最重要的一点是，它将独立处理动画状态，完全自动完成。我们要做的就是告诉状态机速度 (要知道婴儿马里奥是在跑步还是站着)和是否在跳：

让我们选择参数选项卡，单击+在右边，然后添加一个float类型的参数，命名为Speed和另一个bool类型的参数命名Jumping：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171219200.png)
稍后，通过编写以下内容，我们可以在脚本中设置这些参数：

```csharp
GetComponent<Animator>().SetFloat("Speed", 0);
GetComponent<Animator>().SetBool("Jumping", false);
```
我们希望Unity能够根据这些参数自动切换到不同的动画状态。让我们选择Idel状态，右键单击它，选择Make Transition并将白色箭头拖到run状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171307209.png)
之后，我们点击白色箭头，设置当我们的Speed值大于0，就切换run状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171406872.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们还禁用了Has Exit Time属性以避免不必要的状态转换。*

现在我们可以创造另一个Transition从Run回到Idle。这一次，我们将使用条件当Speed小于0.01 (或者换句话说，如果是0):
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171512466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们还禁用了Has Exit Time选项。*

让我们再创建几个过渡：

- Idle到Jump有条件Jumping等于真
- Run到Jump有条件Jumping等于真
- Jump到Idle有条件Jumping等于假

*注：我们将禁用有退出时间为了所有的过渡。*

下面是最后的状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171559160.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注：橙色状态是默认的，或者换句话说：游戏开始后，我们处于橙色状态。*

我们刚刚创建了动画状态机。因此，Unity将自动切换到动画之间，并根据当前状态一遍又一遍地播放它们。
剩下我们要做的就是设置速度和跳，稍后在我们的脚本中使用参数。
那些曾经尝试用脚本手动实现所有这些状态机的人会意识到动画状态机有多么简单。

### 12.婴儿马里奥物理
现在，婴儿马里奥只是游戏世界的一个形象。他不是物理世界的一部分，事情不会与他发生冲突，他也不能到处走动。我们需要添加一个Collider2D使他成为物理世界的一部分，这意味着事物将与婴儿马里奥碰撞，而婴儿马里奥将与其他事物碰撞。

他也应该四处走动。刚体负责物体的重力、速度和其他使物体运动的力。根据经验法则，在物理世界里，所有应该移动的东西都需要一个刚体2D.

让我们选择babymario_0对象中的游戏对象。添加碰撞器和刚体组件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319171819350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们使用了Circle Collider 2D因为它会使运动非常平稳。不会有任何硬的边缘，婴儿马里奥可以被困在。*

### 13.婴儿马里奥运动脚本
婴儿马里奥还是动不了，所以让我们改变一下。
添加一个新脚本PlayerMovement.cs，双击打开它：

```csharp
using UnityEngine;
using System.Collections;

public class PlayerMovement : MonoBehaviour {

    // Use this for initialization
    void Start () {
    
    }
    
    // Update is called once per frame
    void Update () {
    
    }
}
```
让我们先实现水平运动。我们需要两个公共变量moveSpeed和sliding
moveSpeed指定玩家移动的速度，这个sliding考虑到滑动的动作，一旦玩家停止移动，马里奥仍然滑了一点，然后再站住。

```csharp
using UnityEngine;
using System.Collections;

public class PlayerMovement : MonoBehaviour {
    // Movement Properties
    public float moveSpeed = 15;
    [Range(0,1)] public float sliding = 0.9f;

    // Use this for initialization
    void Start () {
    
    }
    
    // Update is called once per frame
    void Update () {
    
    }
}
```
*注：[Range(0，1)]确保sliding 变量只能在以下范围内选择：0和1.*

我们不需要Start和Update函数，删除掉，然后添加一个FixedUpdate函数，关于Update函数和FixedUpdate函数的区别可以看我其他的博客，这边就不再累述：

```csharp
using UnityEngine;
using System.Collections;

public class PlayerMovement : MonoBehaviour {
    // Movement Properties
    public float moveSpeed = 15;
    [Range(0,1)] public float sliding = 0.9f;
    
    void FixedUpdate () {
    
    }
}
```

然后检测玩家的按键输入：

```csharp
void FixedUpdate () {
    // Horizontal Movement
    float h = Input.GetAxis("Horizontal");
}
```

现在我们可以设置velocity让婴儿马里奥动起来，这个velocity是Vector2，这等于当前移动方向乘以移动速度。这里有几个Vertor2的运动方向：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200319172440740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
所以速度就像(1, 0)意思是“向右移动”。

我们只关心水平移动方向，所以我们需要改变的是x坐标的值：

```csharp
Vector2 v = GetComponent<Rigidbody2D>().velocity;
if (h != 0) {
    // Move Left/Right
    GetComponent<Rigidbody2D>().velocity = new Vector2(h * moveSpeed, v.y);
} else {
    // Get slower (Super Mario style sliding motion)
    GetComponent<Rigidbody2D>().velocity = new Vector2(v.x * sliding, v.y);
}
```
*注意：发生的情况是，我们首先检查h是0或者不是。如果是不是0然后玩家想要向左或向右移动。在这种情况下，我们将刚体的水平速度设置为H*速度同时保持垂直速度。如果h是0然后，我们慢慢地降低水平速度滑动因子，并保留垂直的一个，因为它是。我们也可以把速度设为(0, 0)但是，婴儿马里奥会突然停止移动，而不是在停下来之前滑动一点。*

水平运动现在已经起作用了，但是婴儿马里奥还没有动画。
如前所述，我们所要做的就是在脚本中设置Animator的Speed参数的值：

```csharp
// Horizontal Movement
float h = Input.GetAxis("Horizontal");
Vector2 v = GetComponent<Rigidbody2D>().velocity;
if (h != 0) {
    // Move Left/Right
    GetComponent<Rigidbody2D>().velocity = new Vector2(h * moveSpeed, v.y);
} else {
    // Get slower (Super Mario style sliding motion)
    GetComponent<Rigidbody2D>().velocity = new Vector2(v.x * sliding, v.y);
}
GetComponent<Animator>().SetFloat("Speed", h);
```

还没完成呢。我们的h变量可以介于-1(左)及1(右)，但我们的婴儿马里奥的雪碧只包含右侧的动画。我们可以为左侧添加额外的动画，或者只需要编写一些代码在婴儿马里奥跑左边的时候翻转一下：

```csharp
// Horizontal Movement
float h = Input.GetAxis("Horizontal");
Vector2 v = GetComponent<Rigidbody2D>().velocity;
if (h != 0) {
    // Move Left/Right
    GetComponent<Rigidbody2D>().velocity = new Vector2(h * moveSpeed, v.y);
    transform.localScale = new Vector2(Mathf.Sign(h), transform.localScale.y);
} else {
    // Get slower (Super Mario style sliding motion)
    GetComponent<Rigidbody2D>().velocity = new Vector2(v.x * sliding, v.y);
}
GetComponent<Animator>().SetFloat("Speed", Mathf.Abs(h));
```
*注意：我们通过设置婴儿马里奥的缩放值来完成翻转，通过设置scale.x的值Mathf.Sign(h)。看起来很复杂，其实很简单。这个scale.x的值默认情况下是1。如果我们设成-1那么婴儿马里奥就会被翻转。因为h也可能类似于0.5，所以使用Sign(h)，当h为正或为0返回1，为负返回-1。然后，我们设置Speed参数Abs(h)得到绝对值*

因此，我们没有把宝贵的时间花在绘制动画上，而是使用镜像技巧来解决问题。

然后我们将PlayerMovement.cs组件拖到我们的婴儿马里奥对象上：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320143053241.png)
*注意：Sliding是一个滑块，因为我们使用了Range*

如果我们按下Play然后我们就可以让他四处走动了：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320143211615.gif)
好的，让我们实现跳跃！首先，我们需要弄清楚婴儿马里奥目前是否站在地面上。

让我们创建IsGrounded函数来判断是否站在地面上：

```csharp
bool IsGrounded() {
    // noobtuts.com isGrounded function

    // Get Bounds and Cast Range (10% of height)
    Bounds bounds = GetComponent<Collider2D>().bounds;
    float range = bounds.size.y * 0.1f;
    
    // Calculate a position slightly below the collider
    Vector2 v = new Vector2(bounds.center.x,bounds.min.y - range);

    // Linecast upwards
    RaycastHit2D hit = Physics2D.Linecast(v, bounds.center);
    
    // Was there something in-between, or did we hit ourself?
    return (hit.collider.gameObject != gameObject);
}
```
有了这个功能，我们就可以很容易地实现跳。我们将添加另一个变量，来设置跳多高：

```csharp
public float jumpForce = 1200;
```

之后我们会按上键，在这种情况下，我们使用AddForce (当然，只有当他目前站在地面上的时候):

```csharp
// Vertical Movement (Jumping)
bool grounded = IsGrounded();
if(Input.GetKey(KeyCode.UpArrow) && grounded)
    GetComponent<Rigidbody2D>().AddForce(Vector2.up * jumpForce);
```
现在我们可以设置Jumping参数，以便动画状态机知道何时切换状态：

```csharp
// Vertical Movement (Jumping)
bool grounded = IsGrounded();
if(Input.GetKey(KeyCode.UpArrow) && grounded)
    GetComponent<Rigidbody2D>().AddForce(Vector2.up * jumpForce);
GetComponent<Animator>().SetBool("Jumping", !grounded);
```

*注意：我们设置了动画状态机的Jumping参数与grounded。换句话说，每当我们不在地面时，我们都在跳跃。*

下面是最终的脚本：

```csharp
using UnityEngine;
using System.Collections;

public class PlayerMovement : MonoBehaviour {
    // Movement Properties
    public float moveSpeed = 15;
    [Range(0,1)] public float sliding = 0.9f;
    public float jumpForce = 1200;
    
    bool IsGrounded() {
        // noobtuts.com isGrounded function

        // Get Bounds and Cast Range (10% of height)
        Bounds bounds = GetComponent<Collider2D>().bounds;
        float range = bounds.size.y * 0.1f;
        
        // Calculate a position slightly below the collider
        Vector2 v = new Vector2(bounds.center.x,
                                bounds.min.y - range);

        // Linecast upwards
        RaycastHit2D hit = Physics2D.Linecast(v, bounds.center);
        
        // Was there something in-between, or did we hit ourself?
        return (hit.collider.gameObject != gameObject);
    }

    void FixedUpdate () {
        // Horizontal Movement
        float h = Input.GetAxis("Horizontal");
        Vector2 v = GetComponent<Rigidbody2D>().velocity;
        if (h != 0) {
            // Move Left/Right
            GetComponent<Rigidbody2D>().velocity = new Vector2(h * moveSpeed, v.y);
            transform.localScale = new Vector2(Mathf.Sign(h), transform.localScale.y);
        } else {
            // Get slower (Super Mario style sliding motion)
            GetComponent<Rigidbody2D>().velocity = new Vector2(v.x * sliding, v.y);
        }
        GetComponent<Animator>().SetFloat("Speed", Mathf.Abs(h));

        // Vertical Movement (Jumping)
        bool grounded = IsGrounded();
        if(Input.GetKey(KeyCode.UpArrow) && grounded)
            GetComponent<Rigidbody2D>().AddForce(Vector2.up * jumpForce);
        GetComponent<Animator>().SetBool("Jumping", !grounded);
    }
}
```
如果我们按下Play然后我们就可以跳了：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320143743996.gif)
### 14.道具盒
我们的超级马里奥游戏仍然需要那些典型的道具盒。
婴儿马里奥应该跳到他们下面，以便他们生成一个硬币。
在产生硬币后，它们会变成某种固定的盒子，什么也不做。

和往常一样，这一切都是从一个图像开始的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320143942334.png)
*注意：右键另存为，保存到Assets/Sprites文件夹中*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320144023723.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们将图片从项目区拖入到场景中，选中再复制一个，然后分别设置坐标(4, 4)还有一个(7, 4):
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320144117333.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 15.道具盒物理

添加碰撞器和刚体：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320144140274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：我们勾选了刚体的Is Kinematic属性。因为我们的道具盒是静止的，所以就开启Is Kinmatic。如果它像一个玩家一样跑来跑去我们就应该关闭这个Is Kinematic。如果刚体勾选了 Is Kinmatic我们就可以通过transform.position来改变它的位置。如果它没有勾选Is Kinmatic我们可以用刚体的Velocity和AddForce让它移动*

### 16.道具盒的运动
道具盒应该是向上移动，然后再次向下，当玩家顶到它的时候。就像这样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145141724.gif)
有很多方法来实现这种行为。
显而易见的方法是使用脚本的update函数，然后修改transform.position一次又一次地往上走，直到它达到一定的高度
这时它又开始越来越低，一直以同样的速度前进。
由于性能方面的原因，这种方法并不是很好，而且因为移动看起来不太顺利。

相反，我们希望运动看起来非常平稳，通过缓慢的加速，然后更快地向上，再次向下，然后减速，然后再到达底部。可以使用动画曲线：

选中两个道具盒以后，我们选择添加新脚本Box.cs:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145309614.png)
双击打开Box.cs，删除Start和Update函数，因为我们不需要它们，然后添加一个公有的AnimationCurve变量：

```csharp
using UnityEngine;
using System.Collections;

public class Box : MonoBehaviour {

    // The Curve
    public AnimationCurve curve;
}
```
如果我们保存脚本就能看到脚本的曲线变量：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145421442.png)
如果我们单击曲线属性之后，将打开Curve Editor曲线编辑器：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145452151.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们将选择底部的最后一个曲线图像，以创建曲线的前半部分：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145503799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：水平轴将是时间而垂直轴将是y坐标。换句话说，曲线显示的是Y坐标随时间变化。我们还可以看到，曲线开始缓慢上升，但后来上升更快。这正是我们要寻找的运动。*

现在，我们可以把右边的绿色点移到左边更远的地方。(0.25, 1):
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145526559.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：曲线越宽，盒子的移动速度就越慢。如果我们像这样把它挤在一起，它就会移动得更快。*

之后，我们可以双击右边的点来创建一个新的。然后，我们将把新的拖到右下角。(0.5, 0)。现在我们有了描述上下运动的最后一条曲线：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320145547661.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
很好，让我们回到我们的脚本，并利用曲线。
我们将使用OnCollisionEnter2D函数，以确定盒子是否被婴儿马里奥击中。实际上是从底部击中：

```csharp
using UnityEngine;
using System.Collections;

public class Box : MonoBehaviour {

    // The Curve
    public AnimationCurve curve;

    void OnCollisionEnter2D(Collision2D coll) {
        // collision below?
        if (coll.contacts[0].point.y < transform.position.y) {
            // Do stuff...
        }
    }
}
```

如前所述，我们需要改变曲线的位置随着时间的推移，但是使用update函数有一个缺点：即使在移动完成之后，它仍然可以工作(因为在每次Update调用中都会检查所有内容)，所以我们这里使用一种更高效的方式：

那就是使用协程，我们将创建一个函数，实现调用间隔和更新，该函数将在我们完成之后自动移除。(因此没有性能问题).

以下是我们的协程函数：
```csharp
IEnumerator sample() {        
    // go through curve time
    for (float t=0; t < curve.keys[curve.length-1].time; t+=Time.deltaTime) {
        // do stuff...

        // come back next Update
        yield return null;
    }
}

void OnCollisionEnter2D(Collision2D coll) {
    // collision below?
    if (coll.contacts[0].point.y < transform.position.y)
        StartCoroutine("sample");
}
```
*注意：虽然它看起来很奇怪，但它确实不难理解。我们刚刚创建了一个Enumerator类型的函数sampleI，因为这是Coroutines所拥有的类型。然后我们使用for循环来循环播放我们的曲线动画，从0并且以曲线中的最后一个值结束，既curve.keys[curve.length-1].time。我们在每个步骤中增加变量Time.deltaTime，就像我们的Update函数。而yield部分简单地告诉Unity停在这里，下一帧回来。实际上，我们在这里创建了自己的Update函数。*


为了更清楚这一点，下面我们用Update函数演示一下：

```csharp
float t = 0;

void Update() {
    if (t < curve.keys[curve.length-1].time) {
        // do stuff..

        t += Time.deltaTime;
    }
}
```
现在，让我们在这里添加一些力学。我们希望盒子每次移动一点，我们将使用curve.Evaluate函数以求出给定时间的垂直位置：

```csharp
IEnumerator sample() {
    // start position
    Vector2 pos = transform.position;

    // go through curve time
    for (float t=0; t<curve.keys[curve.length-1].time; t+=Time.deltaTime) {
        // move a bit
        transform.position = new Vector2(pos.x, pos.y + curve.Evaluate(t));

        // come back next Update
        yield return null;
    }
}
```
如果我们按下Play现在我们可以看到它真的起作用了：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320150716430.gif)
### 17.产生金币
让我们在脚本中添加另一个变量spawnPrefab，让我们在运动结束的时候生成金币：

```csharp
// The Curve
public AnimationCurve curve;

// The object to spawn
public GameObject spawnPrefab;

IEnumerator sample() {
    // start position
    Vector2 pos = transform.position;

    // go through curve time
    for (float t=0; t<curve.keys[curve.length-1].time; t+=Time.deltaTime) {
        // move a bit
        transform.position = new Vector2(pos.x, pos.y + curve.Evaluate(t));

        // come back next Update
        yield return null;
    }

    // spawn an object if any
    if (spawnPrefab)
        Instantiate(spawnPrefab, transform.position + Vector3.up, Quaternion.identity);
}
```
*注意：当我们播放完动画，就会实例化生成一个spawnPrefab对象到场景中*


我们将在脚本中再添加一个功能。
我们的道具盒子应该只有一次出现道具，之后它应该变成某种固定的盒子。
一般来说，我们需要一个盒子一旦被击中就能把它变成另一个盒子。

我们已经知道如何在盒子的顶部生成一个物体，因此在当前位置产生另一个盒子也同样容易：

```csharp
// The Curve
public AnimationCurve curve;

// The object to spawn
public GameObject spawnPrefab;

// The next box
public GameObject nextPrefab;

IEnumerator sample() {
    // start position
    Vector2 pos = transform.position;

    // go through curve time
    for (float t=0; t<curve.keys[curve.length-1].time; t+=Time.deltaTime) {
        // move a bit
        transform.position = new Vector2(pos.x, pos.y + curve.Evaluate(t));

        // come back next Update
        yield return null;
    }

    // spawn an object if any
    if (spawnPrefab)
        Instantiate(spawnPrefab, transform.position + Vector3.up, Quaternion.identity);

    // spawn next one if any, destroy box
    if (nextPrefab)
        Instantiate(nextPrefab, transform.position, Quaternion.identity);
    Destroy(gameObject);
}
```
太好了，如果我们按下Play跳到道具盒下面，它就会消失。
我们的脚本的伟大之处在于，我们可以使用它在我们的脚本生成各种不同的盒子。
很快就会有更多的事情发生！

### 18.金币
**金币图片**

我们已经只要要在道具盒子上面生成一个道具，现在我们只需要一个金币的图片：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151237814.png)
*注意：右键另存为，保存到项目中的Assets/Sprites文件夹*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151311331.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
将图片拖入到场景中：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151328736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 19.金币的物理

添加碰撞器：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151349782.png)
添加脚本Coin.cs，双击打开，删除Start和Update函数，添加OnTriggerEnter2D函数：

```csharp
using UnityEngine;
using System.Collections;

public class Coin : MonoBehaviour {

    void OnTriggerEnter2D(Collider2D coll) {
        // Destroy the coin
        Destroy(gameObject);
    }
}
```

*注意：对于我们的游戏，这将是加分的地方，为了简单起见，我们不会添加得分功能*

下面是我们的金币GameObject现在的样子：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151529898.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 20.金币预制体
我们不希望硬币从一开始就进入游戏世界。
相反，我们希望每当马里奥跳到盒子下面时，它才会产生出来。
创建一个新的Prefabs文件夹，将金币拖进预制体文件夹，重命名为CoinPrefab
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151726303.png)
然后我们可以把它从场景中删除。既然我们现在有了一个预制件，我们就可以用实例化在我们需要的时候发挥作用。

### 21.生成硬币
为了产生硬币，我们所要做的就是选择问题标记框，然后拖动CoinPrefab进入Spawn Prefab插槽：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151819406.png)
如果我们按下Play然后，我们可以通过跳过一个道具框来收集一些金币：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151842768.gif)
### 22.固定盒子
我们不希望道具盒子在跳过之后完全消失，所以我们需要一个固定盒子，，什么也不做，就像石头一样--地面上的石头。

与往常一样，我们将从绘制一幅图像开始：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320151948966.png)
*注意：右键另存为，导入到项目中Assets/Sprites文件夹*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152027349.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**添加碰撞器**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152045217.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
拖入到Prefabs文件夹，做成预制体：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152104292.png)
之后我们可以再把它从现场删除。

让我们选择道具框，然后拖动fixedPrefab放入Next Prefab插槽：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152138775.png)
如果我们按下Play然后，我们可以看到道具盒子是如何转换为固定盒子的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152207892.gif)
### 23.砖块盒子
让我们添加最后一种类型的盒子，即砖块盒。这只是一堆砖块，没有什么特别的，只是一旦我们跳到他们下面就可以向上和向下移动

让我们先画一个砖块图像：![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152333688.png)
*注意：右键另存为，保存到Assets/Sprites文件夹*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152404112.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
接着摆放到(5,4)的位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152438283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**添加碰撞器和刚体**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152457448.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
添加上Box.cs组件，我们还将指定与我们以前使用的相同的曲线：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152524387.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
现在，如果我们跳到砖块盒子下面，它会向上移动，然后向下移动，然后消失。或者我们可以在原来的地方再生成一块砖盒

让我们将它拖入到Prefabs文件件，命名为bricksPrefab
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152627900.png)
点击brickPrefab预制体，然后拖动bricksPrefab预制体到Next Prefab插槽：

我们还将在场景中再加两块砖块。(6, 4)和(8, 4).

如果我们按下Play现在我们可以看到砖块盒的运动机制：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152830898.gif)
### 24.敌人
**敌人形象**

让我们创造一个非常简单的敌人，只在两点之间来回走动。如果马里奥宝宝跳到敌人身上，那么敌人就死定了。如果敌人走进婴儿马里奥，那么婴儿马里奥就会死去。

敌人需要一个动作动画和一个死亡动画，所以让我们把它们都画成一个图像：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152920168.png)
*注意：右键另存为，保存到Assets/Sprites文件夹*

**导入设置**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320152942733.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注意：Sprite Mode设置成Multiple*

点击Sprite Editor切片编辑器并切片：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153035589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
正如我们对马里奥所做动画步骤那样，我们现在将选择前两片：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153102967.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
然后将它们拖到场景中，以便创建run动画，我们将保存在一个新的EnemyAnimation文件夹：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153126451.png)
我们现在可以对最后两个切片重复这个过程。动画的名字是death
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153140151.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
之后，删除Hierarchy中的enemy_2和EnemyAnimation文件夹中的enemy_2.anim

我们将敌人的位置设置在(16,1):
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153307498.png)
### 25.敌人动画状态机
让我们双击EnemyAnimation文件夹中的enemy_0并查看动画状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153351235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
让我们在EnemyAnimation文件夹中拖动death动画到这里：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153420631.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
让我们选择run状态，然后将其设置为速度到0.5:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153438627.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

现在我们可以创建一个类型为Trigger(这是一种只触发一次的东西)
然后给它起个名字Died:
![Enemy Animator Parameter](https://img-blog.csdnimg.cn/20200320153501343.png)
之后，我们将创建一个新的Transition从run到death的条件切换:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153547753.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
*注：我们还禁用了Has Exit Time*

下面是我们最后的动画状态机：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153618660.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
### 26.敌人的物理
**添加碰撞器和刚体**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153656897.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**移动的目标点**
我们的敌人应该一直在两点之间走动。因此，让我们通过选择GameObject->Create Empty两次，们将命名这些新的游戏对象EnemyDestinationLeft和EnemyDestinationRight：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153750483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
我们将定位左边一个在(15, 1)右边的那个(18, 1)。我们还将在他们两个人中添加一个Gizmo，这样我们就可以在场景中更容易地看到他们：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153809545.png)
现在我们可以看到，这两个目的地位于绿色管道之间：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153821969.png)
我们还将添加一个Collider2D启用Is Trigger，因此稍后我们将收到碰撞信息：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320153846223.png)
### 27.敌人的脚本
让我们添加新脚本Enemy.cs，双击打开，删除Start和Update函数，添加speed变量和dir变量：

```csharp
using UnityEngine;
using System.Collections;

public class Enemy : MonoBehaviour {
    // Movement Speed
    public float speed = 3;

    // Current movement Direction
    Vector2 dir = Vector2.right;
}
```
我们将使用FixedUpdate函数始终
将velocity设置为当前运动方向乘以速度。(这几乎就是速度的定义):

```csharp
void FixedUpdate() {
    // Set the Velocity
    GetComponent<Rigidbody2D>().velocity = dir * speed;
}
```
我们的两个目的地都有触发器，这意味着我们可以使用OnTriggerEnter2D函数，以确定我们是否到达了它们中的任何一个，在这种情况下，我们只需倒转移动方向，并镜像敌人。(为了再次将动画保存到左侧):

```csharp
void OnTriggerEnter2D(Collider2D coll) {
    // Hit a destination? Then move into other direction
    transform.localScale = new Vector2(-1*transform.localScale.x,
                                          transform.localScale.y);

    // And mirror it
    dir = new Vector2(-1 * dir.x, dir.y);
}
```

快好了。
现在，每当敌人和马里奥相撞时，就会发生两件事中的一件：

- 敌人会死 (如果跳到上面)
- 否则马里奥就会死 (如果水平碰撞)

我们可以使用OnCollisionEnter函数通过简单的高度比较来实现此行为：

```csharp
void OnCollisionEnter2D(Collision2D coll) {
    // Collided with BabyMario?
    if (coll.gameObject.name == "BabyMario") {
        // Is the collision above?
        if (coll.contacts[0].point.y > transform.position.y) {
            // ToDo kill self
        } else {
            // ToDo kill BabyMario
        }
    }
}
```
现在我们可以用Destroy摧毁敌人或玩家。
我们还添加了一个小技巧，让婴儿马里奥向上，让敌人下降到屏幕底部，同时播放死亡动画几秒钟：

```csharp
using UnityEngine;
using System.Collections;

public class Enemy : MonoBehaviour {
    // Movement Speed
    public float speed = 3;

    // Current movement Direction
    Vector2 dir = Vector2.right;

    // Upwards push force
    public float upForce = 800;

    void FixedUpdate() {
        // Set the Velocity
        GetComponent<Rigidbody2D>().velocity = dir * speed;
    }

    void OnTriggerEnter2D(Collider2D coll) {
        // Hit a destination? Then move into other direction
        transform.localScale = new Vector2(-1 * transform.localScale.x,
                                                transform.localScale.y);

        // And mirror it
        dir = new Vector2(-1 * dir.x, dir.y);
    }

    void OnCollisionEnter2D(Collision2D coll) {
        // Collided with BabyMario?
        if (coll.gameObject.name == "BabyMario") {
            // Is the collision above?
            if (coll.contacts[0].point.y > transform.position.y) {
                // Play Animation
                GetComponent<Animator>().SetTrigger("Died");

                // Disable collider so it falls downwards
                GetComponent<Collider2D>().enabled = false;
                
                // Push BabyMario upwards
                coll.gameObject.GetComponent<Rigidbody2D>().AddForce(Vector2.up * upForce);
                
                // Die in a few seconds
                Invoke("Die", 5);
            } else {
                // Kill BabyMario
                Destroy(coll.gameObject);
            }
        }
    }

    void Die() {
        Destroy(gameObject);
    }
}
```
如果我们按下Play那么我们现在可以跳到敌人的上面去杀死它：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320154225345.gif)
### 28.摘要
这就是我们的《超级马里奥游戏》Unity开发教程的全部内容了。
是的，有大量的工作，
但是我们也学习到了很多
我们学到了
- 从动画到物理
- 协同程序
- 动画曲线
- 人物运动

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200320154411341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
和往常一样，现在是读者让游戏尽可能有趣的时候了。
- 增加更多的等级
- 相机跟随
- 更多的敌人
- 一些美妙的声音
- 甚至一个公主
