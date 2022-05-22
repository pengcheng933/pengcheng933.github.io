---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D实现圆环进度条
date:     2020-08-21 20:09:00
background-image: https://img-blog.csdnimg.cn/20190617165959212.gif
tags:
- Unity3D
- Unity3D日常开发
---

## 一、前言
今天分享一个制作圆形进度条的方法，原教程比较繁琐，这里给精简一下，更适合于新手

先看下效果吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617165959212.gif)

## 二、原文链接
原文出处：CSDN
原文链接：https://blog.csdn.net/tab_space/article/details/51775163
原文作者：tab_space

## 三、正文

步骤：
### 1、先制作素材
准备一张圆形的图片，中间掏空，保存为png格式
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617170123442.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)

### 2、设置属性

**新建一个image**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617170241138.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**将图片拖进去**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617170319830.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617170332666.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**Image Type改为<font color="red">Filled</font>**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617170417935.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**设置一下**
Fill Method	->Radial 360	
Fill Origin	->Top
Fill Amount-> 1
Clockwise ->False

**新建一个text**
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061717090612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
**位置拖到图片中间**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617170943322.png)

OK 前期工作都准备好了  只需要更改图片的 Fill Amount值就可以实现圆形进度条，有兴趣的同学  可以先拖一下看看效果

### 3、代码控制

新建脚本RingProcess.cs

```csharp
using UnityEngine;
using UnityEngine.UI;

public class RingProcess : MonoBehaviour
{
    //进度条速度
    public float speed;
    //一个图片一个文字
    public Transform m_Image;
    public Transform m_Text;
    //进度控制
    public int targetProcess = 100;
    private float currentAmout = 0;

    void Update()
    {
        if (currentAmout < targetProcess)
        {
            currentAmout += speed;
            if (currentAmout > targetProcess)
                currentAmout = targetProcess;
            m_Text.GetComponent<Text>().text = ((int)currentAmout).ToString() + "%";
            m_Image.GetComponent<Image>().fillAmount = currentAmout / 100.0f;
        }
    }
}

```
### 4、设置参数
将脚本拖到任意物体上面
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061717105851.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
设置参数
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617171133112.png)

OK  ，看看效果吧
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190617171315474.gif)

## 四、项目下载
链接：https://pan.baidu.com/s/1_POXdJKZFBa16jJiY5R7zQ 
提取码：h2vp 
