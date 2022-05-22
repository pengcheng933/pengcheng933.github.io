---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D点击图片生成物体
date:     2020-08-21 20:09:00
background-image: http://cdn.qq764424567.top/ci0.png
tags:
- Unity3D
- Unity3D日常开发
---

## 一、前言
今天给大家分享一个如何点击图片生成物体的脚本，可以把这个脚本稍微封装一下，以后也可以方便使用。
主要试用与点击图片时候响应事件，具体用法还要大家多多摸索

## 二、效果
![这里写图片描述](https://img-blog.csdn.net/20180905145020989?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


## 三、正文

### 步骤：
#### 1.新建2个Image
![这里写图片描述](https://img-blog.csdn.net/20180905145251542?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)![这里写图片描述](https://img-blog.csdn.net/20180905145256792?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)![这里写图片描述](https://img-blog.csdn.net/20180905145301873?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
就改下名字，其他属性都不用改

#### 3.创建两个预制体在Resources文件夹
![这里写图片描述](https://img-blog.csdn.net/20180905145802772?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
名字就没有改（懒..）


#### 2.新建脚本test01.cs

代码如下：

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;

public class test01 : MonoBehaviour
{
    //图片名字
    string imageName;
    //预制体对象
    GameObject part;

    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            //如果获取到对象的话
            if (OnePointColliderObject() != null)
            {
                //给图片名字赋值
                imageName = OnePointColliderObject().name;
                //创建对象
                InstantObject();
            }
        }
    }

    /// <summary>
    /// 点击对象
    /// </summary>
    /// <returns>点击对象获取到对象的名字</returns>
    public GameObject OnePointColliderObject()
    {
        //存有鼠标或者触摸数据的对象
        PointerEventData eventDataCurrentPosition = new PointerEventData(EventSystem.current);
        //当前指针位置
        eventDataCurrentPosition.position = new Vector2(Input.mousePosition.x, Input.mousePosition.y);
        //射线命中之后的反馈数据
        List<RaycastResult> results = new List<RaycastResult>();
        //投射一条光线并返回所有碰撞
        EventSystem.current.RaycastAll(eventDataCurrentPosition, results);
        //返回点击到的物体
        if (results.Count > 0)
            return results[0].gameObject;
        else
            return null;
    }

    public void InstantObject()
    {
        switch (imageName)
        {
            case "Image_1":
                GameObject obj01 = (GameObject)Resources.Load("Cube");
                part = Instantiate(obj01, Vector3.zero, obj01.transform.rotation);
                break;
            case "Image_2":
                GameObject obj02 = (GameObject)Resources.Load("Sphere");
                part = Instantiate(obj02, Vector3.up, obj02.transform.rotation);
                break;
            default:
                break;
        }
    }
}


```

代码比较简单，就不多说了，都有注释。
主要讲一下<font color="red">OnePointColliderObject</font>这个函数中的

- <font color="red">EventSystem.current.RaycastAll(eventDataCurrentPosition, results);</font>
- <font color="red">RaycastAll</font>的主要特性就是使用光线投射碰撞：在还没有发生真正的物理碰撞之前，就响应碰撞。
- public void RaycastAll(PointerEventData eventData, List<RaycastResult> raycastResults);


OK，大家可以试一下，有什么新奇的点子也可以留言哦
