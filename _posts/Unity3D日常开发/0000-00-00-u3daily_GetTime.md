---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D 获取到运行时间，然后实时显示出来
date:     2020-08-21 20:09:00
background-image: https://img-blog.csdnimg.cn/20200106100336942.gif
tags:
- Unity3D
- Unity3D日常开发
---

## 一、前言
分享一下如何获取到运行时间，然后实时显示出来

## 二、效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200106100336942.gif)
**Github地址：https://github.com/764424567/Demo_GetTime
可以直接下载源代码**

## 三、正文
代码：

```csharp
using UnityEngine;
using UnityEngine.UI;

public class GetTime : MonoBehaviour
{
    int hour;
    int minute;
    int second;
    int millisecond;
    // 已经花费的时间 
    float timeSpend = 0.0f;
    // 显示时间区域的文本 
    Text text_timeSpend;

    void Start()
    {
        text_timeSpend = GetComponent<Text>();
    }

    void Update()
    {
        timeSpend += Time.deltaTime;

        hour = (int)timeSpend / 3600;
        minute = ((int)timeSpend - hour * 3600) / 60;
        second = (int)timeSpend - hour * 3600 - minute * 60;
        millisecond = (int)((timeSpend - (int)timeSpend) * 1000);

        text_timeSpend.text = string.Format("{0:D2}:{1:D2}:{2:D2}.{3:D3}", hour, minute, second, millisecond);
    }
}

```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190524090720764.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
把这个脚本添加到任意一个text文本上就行了

