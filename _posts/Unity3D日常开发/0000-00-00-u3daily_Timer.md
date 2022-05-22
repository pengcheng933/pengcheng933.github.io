---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D Unity3D做计时器工具
date:     2020-08-21 20:09:00
background-image: https://img-blog.csdnimg.cn/20191231161127483.gif
tags:
- Unity3D
- Unity3D日常开发
---

## 一、前言
今天分享一下如何基于Unity3D做计时器工具，为了方便演示，使用了UGUI的Text，代码简单具有拓展性，然后有什么错误或者意见也欢迎大家给我提出来。微信二维码已经显示在博客主页，有想要沟通学习的，项目外包的都可以加一下。

分享一下我另一篇关于时间计时的文章：
[【Unity3D】获取到游戏时间，并显示出来](https://blog.csdn.net/q764424567/article/details/88688113)

## 二、效果图
计时器效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191231161127483.gif)
倒计时效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191231161150169.gif)
## 三、本文链接
本文链接：https://blog.csdn.net/q764424567/article/details/103784853
GitHub项目源码下载：https://github.com/764424567/Demo_Timer

## 四、代码

```csharp
using UnityEngine;
using UnityEngine.UI;

public class Test_1 : MonoBehaviour
{
    string m_Mins = "0";
    string m_Sec = "0";
    float m_TempMins = 0;
    float m_TempSec = 0;
    bool m_IsTimed = true;
    bool m_IsCountDown = true;

    private void Awake()
    {
        //计时器
        //SetTimed("00:00");

        //倒计时
        SetTimed("10:00");
        string TimeStr = transform.GetComponent<Text>().text;
        string[] TimeStrSplit = TimeStr.Split(':');
        m_TempMins = float.Parse(TimeStrSplit[0]);
        m_TempSec = float.Parse(TimeStrSplit[1]);
        m_IsCountDown = false;
    }

    private void FixedUpdate()
    {
        if (m_IsCountDown)//计时器
        {
            if (m_IsTimed)
            {
                if (transform.GetComponent<Text>().text == "09:59")
                {
                    transform.GetComponent<Text>().text = "10:00";
                    m_Mins = "00";
                    m_Sec = "00";
                    m_TempMins = 0;
                    m_TempSec = 0;
                    m_IsTimed = false;
                }
                else
                {
                    if (m_TempSec >= 9)
                    {
                        m_Sec = (m_TempSec += 1).ToString();
                        if (m_TempSec == 60)
                        {
                            m_Sec = "00";
                            m_TempSec = 0;
                            m_TempMins += 1;
                        }
                    }
                    else
                    {
                        m_Sec = "0" + (m_TempSec += 1).ToString();
                    }
                    m_Mins = "0" + m_TempMins.ToString();
                    transform.GetComponent<Text>().text = m_Mins + ":" + m_Sec;
                }
            }
        }
        else//倒计时
        {
            if (m_IsTimed)
            {
                if (m_TempSec <= 10)
                {
                    if (m_TempSec == 0)
                    {
                        if (m_TempMins == 0)
                        {
                            transform.GetComponent<Text>().text = "00:00";
                            m_IsTimed = false;
                        }
                        else
                        {
                            m_TempSec = 60;
                            m_TempMins -= 1;
                            if (m_TempMins <= 10)
                            {
                                
                                m_Mins = "0" + m_TempMins.ToString();
                            }
                            else
                            {
                                m_Mins = m_TempMins.ToString();
                            }
                        }
                        m_Sec = m_TempSec.ToString();
                    }
                    else
                    {
                        m_Sec = "0" + (m_TempSec -= 1).ToString();
                    }
                }
                else
                {
                    m_Sec = (m_TempSec -= 1).ToString();
                }
                transform.GetComponent<Text>().text = m_Mins + ":" + m_Sec;
            }
        }
    }

    public void SetTimed(string time)
    {
        transform.GetComponent<Text>().text = time;
    }
}

```

