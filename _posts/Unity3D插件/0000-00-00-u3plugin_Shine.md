---
layout:   blog
istop:	  false
book:	  false
u3game:	  false
u3plugin: true
ico:	code
category: Unity3D-Plugin
title:    【Unity3D】发光插件
date:     2020-08-21 21:09:00
background-image: https://img-blog.csdnimg.cn/20190520092832847.gif
tags:
- Unity3D
- Unity3D插件
---

## 一、前言
本篇文章讲的是如何让3D物体放光的方法

## 二、效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190301162136680.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190520092832847.gif)

## 三、实现
这个是一个插件，但是主要就是这几个脚本加Shader
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190520092803193.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
资源包下载：
链接：https://pan.baidu.com/s/1mfZWPsUsbgvH2ACUTBW7Hg 
提取码：5207 
或者
https://download.csdn.net/download/q764424567/11188790

### 操作步骤

1.主摄像机上面添加HighlightingEffect脚本
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190301162629324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=,size_16,color_FFFFFF,t_70)
2.要发光的物体上面添加这两个脚本
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190520095714581.png)

OK，搞定了

