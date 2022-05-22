---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D 场景的淡入淡出效果实现
date:     2020-08-21 20:09:00
background-image: http://cdn.qq764424567.top/fade0.gif
tags:
- Unity3D
- Unity3D日常开发
---


# Unity3d 场景的淡入淡出效果实现
## 思路
1.  用UGUI设计一张全屏的纯色图片
2.  控制图片的Alpha值，来实现淡入淡出的效果


效果展示

![这里写图片描述](https://img-blog.csdn.net/20180608111743782?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

## 实现
4.  先新建一张图片，设置锚点为全屏
![这里写图片描述](https://img-blog.csdn.net/20180608110807513?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
设置颜色值
![这里写图片描述](https://img-blog.csdn.net/20180608110819773?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
![这里写图片描述](https://img-blog.csdn.net/20180608110906670?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3E3NjQ0MjQ1Njc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
5. 新建脚本Fade_Control

```csharp
using UnityEngine;
using UnityEngine.UI;


//状态效果值
public enum FadeStatuss
{
    FadeIn,
    FadeOut
}

public class Fade_Control : MonoBehaviour
{
	//设置的图片
    public Image m_Sprite;
    //透明值
    private float m_Alpha;
    //淡入淡出状态
    private FadeStatuss m_Statuss;
    //效果更新的速度
    public float m_UpdateTime;
    //场景名称
    public string m_ScenesName;

    // Use this for initialization
    void Start()
    {
	    //默认设置为淡入效果
        m_Statuss = FadeStatuss.FadeIn;
    }

    // Update is called once per frame
    void Update()
    {
	    //控制透明值变化
        if (m_Statuss == FadeStatuss.FadeIn)
        {
            m_Alpha += m_UpdateTime * Time.deltaTime;
        }
        else if (m_Statuss == FadeStatuss.FadeOut)
        {
            m_Alpha -= m_UpdateTime * Time.deltaTime;
        }
        UpdateColorAlpha();
    }

    void UpdateColorAlpha()
    {
	    //获取到图片的透明值
        Color ss = m_Sprite.color;
        ss.a = m_Alpha;
        //将更改过透明值的颜色赋值给图片
        m_Sprite.color = ss;
        //透明值等于的1的时候 转换成淡出效果
        if (m_Alpha > 1f)
        {
            m_Alpha = 1f;
            m_Statuss = FadeStatuss.FadeOut;
        }
        //值为0的时候跳转场景
        else if (m_Alpha < 0)
        {
            SceneManager.LoadScene(m_ScenesName);
        }
    }
}

```
OK，有一点不完美的是在屏幕亮了之后才加载场景，应该是在正在亮的时候就加载场景，在以后再完善一下吧
