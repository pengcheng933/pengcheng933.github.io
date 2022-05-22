---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D 实现“使用次数限制以及时间限制功能”
date:     2020-08-21 20:09:00
background-image: http://cdn.qq764424567.top/monon.png
tags:
- Unity3D
- Unity3D日常开发
- 2020
---


## 一、前言
在使用Unity进行软件开发的时候，会遇到实现程序的使用次数限制，以及使用的时间区间限制，说白就是保护程序的一种措施。我们用的方法是，新建注册表，增加键值对，修改键值，完成对程序的使用权限控制。当然还有更加安全的方法，包括获取硬盘编号，还有电子狗加密等等，这些就以后讨论。

<ul>
<li>
<p>【Unity3D】实现“使用次数限制以及时间限制功能”</p>
<ul>
<li>
<p><a href="#1.1" rel="nofollow">一、时间限制</a></p>
</li>
<li>
<p><a href="#1.1" rel="nofollow">二、次数限制</a></p>
</li>
<li>
<p><a href="#1.1" rel="nofollow">三、同时控制时间和次数</a></p>
</li>
</ul>
</li>
</ul>

## 二、参考文章
Unity 限时使用 限制试用时间和使用次数
https://blog.csdn.net/zjh_368/article/details/87920383
作者：紫阳_368

<h1 id="1.1" >

## 三、时间限制
**修改Start()函数里的<font color="blue">minTime</font>和<font color="blue">maxTime</font>时间即可。限制时间也可精确到秒，比如：
<font color="greed">DateTime minTime = Convert.ToDateTime("2019-4-23 12:22:05");</font>**


代码：

```csharp
using System;
using UnityEngine;

public class SetUserTime : MonoBehaviour
{
    //用户是否超过使用日期
    bool Islate = false;

    // Use this for initialization
    void Start()
    {
        //===（比如8月1日开始计算，到8月8日结束）
        //小于minTime 时间或者大于maxTime时间 ，将不可使用
        DateTime minTime = Convert.ToDateTime("2019-8-1 15:29:00");
        DateTime maxTime = Convert.ToDateTime("2019-8-8 15:29:00");
        if (minTime > DateTime.Now || DateTime.Now > maxTime)
        {
            //不在使用时间内，会直接退出程序
            Islate = true;
        }
        SetPlayUseNumber();
    }

    /// <summary>
    /// 设置用户使用次数
    /// </summary>
    void SetPlayUseNumber()
    {
        //异常捕捉，如果发生异常，比如闪退，限制改为false
        try
        {
            //限制使用时间，如果不在这个区间内,直接退出程序
            if (Islate)
            {
                Invoke("OnExit", 2);//延时退出，可在退出前显示提示消息
            }
        }
        catch
        {
            Islate = false;
        }
    }

    //出处程序
    private void OnExit()
    {
        Application.Quit();
    }
}
```
</h1>
<h1 id="1.2" >

## 四、次数限制

SetPlayUseNumber()为限制次数方法，修改键值名就可以重新计算("UseTime")

本脚本是限制时间和次数的搭配使用，可自行修改。

脚本：

```csharp
using Microsoft.Win32;
using UnityEngine;

public class SetUserTime1 : MonoBehaviour
{
    //最大使用次数
    int MaxUsageCount = 3;

    void Start()
    {
        SetPlayUseNumber();
    }

    /// <summary>
    /// 设置用户使用次数
    /// </summary>
    void SetPlayUseNumber()
    {
        //创建键值对
        RegistryKey RootKey, RegKey;
        //项名为：HKEY_CURRENT_USER\Software
        RootKey = Registry.CurrentUser.OpenSubKey("SOFTWARE", true);
        //打开子项：HKEY_CURRENT_USER\Software\MyRegDataApp
        if ((RegKey = RootKey.OpenSubKey("TestToControlUseTime", true)) == null)
        {
            RootKey.CreateSubKey("TestToControlUseTime");               //不存在，则创建子项
            RegKey = RootKey.OpenSubKey("TestToControlUseTime", true);  //打开键值
            RegKey.SetValue("UseTime7", (object)MaxUsageCount);         //创建键值，存储最大可使用次数
            return;
        }
        //异常捕捉，如果出现程序异常，比如闪退，次数更新为开始设置的最大使用次数
        try
        {
            object usetime = RegKey.GetValue("UseTime7");        //读取键值，可使用次数
            print("还可以使用:" + usetime + "次");
            //使用次数减1
            int newtime = int.Parse(usetime.ToString()) - 1;
            if (newtime < 0)
            {
                //到期退出程序
                RegKey.SetValue("UseTime7", (object)newtime);
                Invoke("OnExit", 2);//延时退出，可在退出前显示提示消息
            }
            else
            {
                RegKey.SetValue("UseTime7", (object)newtime);    //更新键值，可使用次数减1
            }
        }
        catch
        {
            RegKey.SetValue("UseTime7", (object)MaxUsageCount);
            print("更新使用次数");
        }
    }

    /// <summary>
    /// 退出程序
    /// </summary>
    private void OnExit()
    {
        Application.Quit();
    }
}
```
</h1>
<h1 id="1.3" >

## 五、同时控制时间和次数

```csharp
using Microsoft.Win32;
using System;
using UnityEngine;

public class SetUserTime2 : MonoBehaviour
{
    //最大使用次数
    int MaxUsageCount = 3;
    //用户是否超过使用日期
    bool Islate = false;

    void Start()
    {
        //===（比如8月1日开始计算，到8月8日结束）
        //小于minTime 时间或者大于maxTime时间 ，将不可使用
        DateTime minTime = Convert.ToDateTime("2019-8-1 15:29:00");
        DateTime maxTime = Convert.ToDateTime("2019-8-8 15:29:00");
        if (minTime > DateTime.Now || DateTime.Now > maxTime)
        {
            //不在使用时间内，会直接退出程序
            Islate = true;
        }
        SetPlayUseNumber();
    }

    /// <summary>
    /// 设置用户使用次数
    /// </summary>
    void SetPlayUseNumber()
    {
        //创建键值对
        RegistryKey RootKey, RegKey;
        //项名为：HKEY_CURRENT_USER\Software
        RootKey = Registry.CurrentUser.OpenSubKey("SOFTWARE", true);
        //打开子项：HKEY_CURRENT_USER\Software\MyRegDataApp
        if ((RegKey = RootKey.OpenSubKey("TestToControlUseTime", true)) == null)
        {
            RootKey.CreateSubKey("TestToControlUseTime");               //不存在，则创建子项
            RegKey = RootKey.OpenSubKey("TestToControlUseTime", true);  //打开键值
            RegKey.SetValue("UseTime7", (object)MaxUsageCount);         //创建键值，存储最大可使用次数
            return;
        }
        //异常捕捉，如果出现程序异常，比如闪退，次数更新为开始设置的最大使用次数
        try
        {
            object usetime = RegKey.GetValue("UseTime7");        //读取键值，可使用次数
            print("还可以使用:" + usetime + "次");
            //使用次数减1
            int newtime = int.Parse(usetime.ToString()) - 1;
            if (newtime < 0 || Islate)
            {
                //到期退出程序
                RegKey.SetValue("UseTime7", (object)newtime);
                Invoke("OnExit", 2);//延时退出，可在退出前显示提示消息
            }
            else
            {
                RegKey.SetValue("UseTime7", (object)newtime);    //更新键值，可使用次数减1
            }
        }
        catch
        {
            RegKey.SetValue("UseTime7", (object)MaxUsageCount);
            Islate = false;
            print("更新使用次数");
        }
    }

    /// <summary>
    /// 退出程序
    /// </summary>
    private void OnExit()
    {
        Application.Quit();
    }
}
```

