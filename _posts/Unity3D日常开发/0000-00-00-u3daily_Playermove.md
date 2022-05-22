---
layout: blog
istop:	false
book:	true
u3daily:  true
category: Unity3D-Daily
title:  Unity3D中控制人物移动
date:   2020-08-21 20:09:00
background-image: http://cdn.qq764424567.top/playermove1.gif
tags:
- Unity3D
- Unity3D日常开发
---

## 一、前言

网上关于角色移动的文章太多太多了，就我自己整理的时候都发现写了好多篇（因为有不同的方案），今天就将目前已知的移动角色的方案总结出来，毕竟是一个资源整合的时代，谁也不想找个角色移动的脚本都要找好几篇文章对吧

目前可以划分为三个方面

- 角色移动到鼠标点击的位置
- 键盘控制角色移动（其他的比如游戏手柄也算键盘、HTC手柄 也算键盘）
- 手机端转盘控制角色移动

其他的比如摄像机跟随移动这个可以作为拓展

## 二、角色移动到鼠标点击的位置

代码：

```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;
    Vector3 tempPoint = new Vector3(0, 0, 0);

    void Update()
    {
        PlayerMove_FollowMouse();
    }

    //角色移动到鼠标点击的位置
    public void PlayerMove_FollowMouse()
    {
        
        //右键点击
        if (Input.GetMouseButtonDown(1))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            RaycastHit hitInfo;
            if (Physics.Raycast(ray,out hitInfo))
            {
                tempPoint = hitInfo.point;
            }
        }
        float step = 10 * Time.deltaTime;
        Player.transform.localPosition = Vector3.MoveTowards(Player.transform.localPosition, tempPoint, step);
        Player.transform.LookAt(tempPoint);
    }
}
```

效果图：

![](http://cdn.qq764424567.top/playermove1.gif)


## 三、键盘控制角色移动（其他的比如游戏手柄也算键盘、HTC手柄 也算键盘）

键盘移动也有好几种方案，这些都会写到

### 3-1、键盘通过Transform组件 控制角色移动

代码：
```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;
    public float m_speed = 5f;

    void Update()
    {
        //键盘控制移动
        PlayerMove_KeyTransform();
    }

    //通过Transform组件 键盘控制移动
    public void PlayerMove_KeyTransform()
    {
        if (Input.GetKey(KeyCode.W) | Input.GetKey(KeyCode.UpArrow)) //前
        {
            Player.transform.Translate(Vector3.forward * m_speed * Time.deltaTime);
        }
        if (Input.GetKey(KeyCode.S) | Input.GetKey(KeyCode.DownArrow)) //后
        {
            Player.transform.Translate(Vector3.forward * -m_speed * Time.deltaTime);
        }
        if (Input.GetKey(KeyCode.A) | Input.GetKey(KeyCode.LeftArrow)) //左
        {
            Player.transform.Translate(Vector3.right * -m_speed * Time.deltaTime);
        }
        if (Input.GetKey(KeyCode.D) | Input.GetKey(KeyCode.RightArrow)) //右
        {
            Player.transform.Translate(Vector3.right * m_speed * Time.deltaTime);
        }
    }
}
```

效果图：

![](http://cdn.qq764424567.top/playermove2.gif)


另一种写法，效果一致：

代码：
```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;
    public float m_speed = 5f;

    void Update()
    {
        //键盘控制移动
        PlayerMove_KeyTransform2();
    }

    //通过Transform组件 键盘控制移动 另一种写法
    public void PlayerMove_KeyTransform2()
    {
        float horizontal = Input.GetAxis("Horizontal"); //A D 左右
        float vertical = Input.GetAxis("Vertical"); //W S 上 下

        Player.transform.Translate(Vector3.forward * vertical * m_speed * Time.deltaTime);//W S 上 下
        Player.transform.Translate(Vector3.right * horizontal * m_speed * Time.deltaTime);//A D 左右
    }
}

```
效果图：

![](http://cdn.qq764424567.top/playermove2.gif)

### 3-2、键盘通过Rigidbody组件 控制角色移动

通过Rigidbody组件 键盘控制移动 Velocity移动 角色身上需要挂载Rigidbody组件

代码：
```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;

    void Update()
    {
        PlayerMove_KeyRighidbody();
    }

    //通过Rigidbody组件 键盘控制移动 Velocity移动 角色身上需要挂载Rigidbody组件
    public void PlayerMove_KeyRighidbody()
    {
        float horizontal = Input.GetAxis("Horizontal"); //A D 左右
        float vertical = Input.GetAxis("Vertical"); //W S 上 下
        //这个必须分开判断 因为一个物体的速度只有一个
        if (Input.GetKey(KeyCode.W) | Input.GetKey(KeyCode.S))
        {
            Player.GetComponent<Rigidbody>().velocity = Vector3.forward * vertical * m_speed;
        }
        if (Input.GetKey(KeyCode.A) | Input.GetKey(KeyCode.D))
        {
            Player.GetComponent<Rigidbody>().velocity = Vector3.right * horizontal * m_speed;
        }
    }
}
```

通过Rigidbody组件 键盘控制移动 AddForce控制移动 角色身上需要挂载Rigidbody组件

代码：

```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;

    void Update()
    {
        PlayerMove_KeyRighidbody2();
    }

    //通过Rigidbody组件 键盘控制移动 AddForce控制移动 角色身上需要挂载Rigidbody组件
    public void PlayerMove_KeyRighidbody2()
    {
        float horizontal = Input.GetAxis("Horizontal"); //A D 左右
        float vertical = Input.GetAxis("Vertical"); //W S 上 下

        Player.GetComponent<Rigidbody>().AddForce(Vector3.forward * vertical * m_speed);
        Player.GetComponent<Rigidbody>().AddForce(Vector3.right * horizontal * m_speed);
    }
}
```

效果图：

![](http://cdn.qq764424567.top/playermove2.gif)


### 3-3、键盘通过CharacterController组件 控制角色移动

通过CharacterController组件 键盘移动物体 SimpleMove控制移动

代码：
```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;

    void Update()
    {
        PlayerMove_KeyCharacterController();
    }

    //通过CharacterController组件 键盘移动物体 SimpleMove控制移动
    public void PlayerMove_KeyCharacterController()
    {
        float horizontal = Input.GetAxis("Horizontal"); //A D 左右
        float vertical = Input.GetAxis("Vertical"); //W S 上 下

        Player.GetComponent<CharacterController>().SimpleMove(transform.forward * vertical * m_speed);
    }
}

```

通过CharacterController组件 键盘移动物体 Move控制移动

代码：

```csharp
using UnityEngine;

public class Test : MonoBehaviour
{
    public GameObject Player;

    void Update()
    {
        PlayerMove_KeyCharacterController2();
    }

    //通过CharacterController组件 键盘移动物体 Move控制移动
    public void PlayerMove_KeyCharacterController2()
    {
        float horizontal = Input.GetAxis("Horizontal"); //A D 左右
        float vertical = Input.GetAxis("Vertical"); //W S 上 下
        float moveY = 0;
        float m_gravity = 10f;
        moveY -= m_gravity * Time.deltaTime;//重力
        Player.GetComponent<CharacterController>().Move(new Vector3(horizontal, moveY, vertical) * m_speed * Time.deltaTime);
    }
}

```

## 四、手机端转盘控制角色移动

这个可以使用EasyTouch插件，这个插件的使用以后再单独编写吧