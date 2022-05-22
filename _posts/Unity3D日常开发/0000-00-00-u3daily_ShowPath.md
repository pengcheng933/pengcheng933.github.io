---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D 自动寻路并且动态显示路线
date:     2020-08-21 20:09:00
background-image: http://cdn.qq764424567.top/sp0.gif
tags:
- Unity3D
- Unity3D日常开发
---

<a color="red">在Unity3d中实现点击目标点，然后出现引路线段，动态更新线段等功能</a>
![这里写图片描述](http://img.blog.csdn.net/20171128090547661?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcTc2NDQyNDU2Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

<h1>主要用到组件：</h1>
<h2>NavMeshAgent</h2>
![这里写图片描述](http://img.blog.csdn.net/20171128090515489?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcTc2NDQyNDU2Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

参数就不全部说明了，就说几个重要的吧
Steering->Speed
<1>这个是设置自动寻路的速度的，可以把这个值设置成0，然后就会光显示路线，而不自动寻路了。
<2>也可以随便设置一个值，然后就会显示路线，而且还会自动寻路

Steering->Stopping Distance
<1>这个的话就是寻路到目标点之后，距离目标点还有多少的距离，也就是停止距离
<2>如果目标点有碰撞体的话最后把这个值调大一点，不然会一直寻路，往这个方向挤

Path Finding->Area Mask
<1>可以行走的区域，这个再配合
![这里写图片描述](http://img.blog.csdn.net/20171128091729463?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcTc2NDQyNDU2Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![这里写图片描述](http://img.blog.csdn.net/20171128091823512?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcTc2NDQyNDU2Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
这2个使用。先添加Areas层，然后在Object->Navgation Area->设置Areas层
<2>这个可以运用到dota游戏中，小兵自动3路寻路

<h2>LineRenderer组件</h2>
这个的话主要是用来在Game视图中画线段
![这里写图片描述](http://img.blog.csdn.net/20171128092152376?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcTc2NDQyNDU2Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
首先要设置一下
LineRenderer->Materials
材质要设置一下，不然会显示材质丢失，就是那个紫色的一团


LineRenderer->Parameters->StartWidth 
LineRenderer->Parameters->EndWidth
这两个是设置开始宽度和结束宽度。如果先要让线段粗一点可以设置值大一些



<h1>然后上代码</h1>

```
using UnityEngine;
using System.Collections;

public class Nav : MonoBehaviour
{
    private NavMeshAgent agent;
    public Transform target;
    private LineRenderer lineRenderer;
    // Use this for initialization
    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
        lineRenderer = gameObject.GetComponent<LineRenderer>();
    }

    // Update is called once per frame
    void Update()
    {
        //设置自动寻路的目标点
        agent.SetDestination(target.position);
        //储存自动寻路的点的坐标
        Vector3[] path = agent.path.corners;
        //线段整体y轴加1个单位
        for (int i = 0; i < path.Length; i++)
        {
            path[i] = path[i] + new Vector3(0, 1, 0);
        }
        //设置定点的数量
        lineRenderer.SetVertexCount(path.Length);
        for (int i = 0; i < path.Length; i++)
        {
            //设置线段的路劲
            lineRenderer.SetPosition(i, path[i]);
        }
    }
}

```

需要现在场景中烘培出来路径，然后在对象上加上NavMeshAgent组件和LineRenderer组件
![这里写图片描述](https://img-blog.csdn.net/20180525100642443?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

>Agent Type 

自动寻路的类型
>Base Offset


基本偏移，碰撞几何体相对于实际几何体垂直的偏移
>Speed


移动的速度，这个数值越大移动的速度越快
>Angular Speed


转角的移动速度
>Acceleration


加速度
>Stopping Distance


停止的间隔，在离目标点多远的距离停下来的意思
>Auto Braking


自动停止
>Radius


自动寻路的半径，可以与实际物体半径不一致
>Height


自动寻路的高度，可以与实际物体高度不一致
>Quality


躲避的等级，等级越高躲避越好，相对于计算量也会大一些
>Auto Traverse OffMesh


自动穿过OffMesh
>Auto Repath


自动重复
>Area Mask


就是当前对象可以通过的网格路径，这个是在Naviagtion中设置

<h1>Line Renderer</h1>

![这里写图片描述](https://img-blog.csdn.net/20180525102221795?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
这个就介绍几个比较重要的属性吧
Materials
这个是设置线段的材质，这个不设置的话就会显示成紫色（就是材质丢失的状态）
Width
就是线段的宽度
Positions
这个就是设置线段的路径的
