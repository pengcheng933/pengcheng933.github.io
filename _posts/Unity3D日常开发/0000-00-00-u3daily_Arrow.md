---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D箭头指向效果
date:     2020-08-21 20:09:00
background-image: https://img-blog.csdnimg.cn/20190227112309192.gif
tags:
- Unity3D
- Unity3D日常开发
---

## 一、前言
本文主要实现一个箭头指向的作用，现在看一下效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112309192.gif)

## 二、需要用到的资源
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112432309.png)
都是png文件，上传到百度云盘了 
链接：https://pan.baidu.com/s/1opQYzSNrXKboM3eFWEb-qQ 
提取码：avvu 

## 三、正文
1.新建一个Plane
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112628134.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
2.创建材质arrow
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112644407.png)
从下载的图片包中随便找一张图片拖进去，然后Shader改为Unlit/Transparent

3.将材质球赋给Plant
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112811834.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112804641.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

4.编写脚本Arrow_Control.cs

```csharp
using UnityEngine;

public class Arrow_Control : MonoBehaviour
{
    //所有的图片路径
    private string[] m_Url;
    //图片名称
    private string m_Name = "Arrow/JianTou_";
    //切换图片的时间
    private float m_Time = 0;
    //图片计数器
    private int TeInt = 0;
    //切换图片的间隔比例
    private float m_Fps = 25;
    //自身的Renderer组件
    private Renderer m_Image;

    void Start()
    {
        //初始化路径字段
        m_Url = new string[27];
        //获取到自身的Renderer
        m_Image = gameObject.GetComponent<Renderer>();
    }


    void Update()
    {
        m_Time += Time.deltaTime;
        // 0.04秒更换一次图片
        if (m_Time >= 1.0 / m_Fps)
        {
            TeInt++;
            m_Time = 0;
        }
        //计数器读取到最后一张图片之后
        if (TeInt > m_Url.Length - 1)
        {   
            TeInt = 0;
        }
        //数组赋值，图片的名字
        m_Url[TeInt] = m_Name + TeInt.ToString();
        //赋值
        m_Image.material.mainTexture = Resources.Load(m_Url[TeInt]) as Texture2D;
    }
}


```

5.将脚本赋值给Plant
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112928323.png)
6.然后在工程中，新建文件夹，名字为Resources，在Resources新建子文件夹Arrow
将上面的图片资源全部放到这个文件夹中。

完成了 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190227112309192.gif)
