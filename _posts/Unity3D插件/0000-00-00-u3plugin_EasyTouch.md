---
layout:   blog
istop:	  false
book:	  false
u3game:	  false
u3plugin: true
ico:	code
category: Unity3D-Plugin
title:    【Unity3D】EasyTouch插件
date:     2020-08-21 21:09:00
background-image: https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY0NjI2NDY4?x-oss-process=image/format,png
tags:
- Unity3D
- Unity3D插件
---

## 一、前言
这篇文章参考了很多博客，然后加入了一些自己的理解，从了解到深入都有比较详细的例子参考，有不对的地方希望大家可以指出来。thank！

## 二、参考资料
Unity3D教程之EasyTouch插件
http://www.newbieol.com/information/564.html
Unity3D EasyTouch 初步使用教程（详细）
http://blog.csdn.net/lifeonelive/article/details/47974905
Unity插件EasyTouch学习记录
http://blog.csdn.net/crazyape/article/details/71597452
【Unity插件】EasyTouch5教程
http://blog.csdn.net/weixin_38158625/article/details/72673294
Unity插件——EasyTouch的使用
http://blog.csdn.net/u014086857/article/details/52087379


## 三、下载链接
第一：http://www.newbieol.com
第二：https://www.assetstore.unity3d.com/cn/#!/content/3322
第三：http://download.csdn.net/detail/s10141303/6962919
第四：http://pan.baidu.com/s/1o6Bt2bS

## 四、使用说明

**创建步骤：**

点击菜单栏的Tools->Hedgehog Team->Easy Touch->Extensions->Add a new Joystick 完成以上骤，此时就会在Game试图左下角看到创建了虚拟遥感的实例。

![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY0NjI2NDY4?x-oss-process=image/format,png)
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY0NjM0ODI2?x-oss-process=image/format,png)
　　
**属性面板的组件预览**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY0ODA1NDkx?x-oss-process=image/format,png)
**属性面板组件参数
joystick properties**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY1MjMzNDk0?x-oss-process=image/format,png)
oystick properties下的Joystick name的命名很重要（名字要设置好，脚本代码可以根据这个名字找到是哪个摇杆触发的），等下脚本要用到它。
**joystick position & size**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY1MjQ2MzQ1?x-oss-process=image/format,png)
**joystick axes properties & events**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY1MjU0MzY3?x-oss-process=image/format,png)
Interaction type(事件驱动类型）选择Event Notification。
**joystick textures**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAyMTY1MzAzMDc4?x-oss-process=image/format,png)
参数Speed，控制的是摇杆的x，y轴向的灵敏度，都改为1即可。

以上设置完成后，我们新建一个脚本Move.cs

添加如下代码。

```csharp
using UnityEngine;
using System.Collections;

public class Move : MonoBehaviour {

        void OnEnable()  

        {    
               EasyJoystick.On_JoystickMove += OnJoystickMove;  
        }  
                       //  此函数是摇杆移动中所要处理的事
        void OnJoystickMove(MovingJoystick move)  
          {    
              if (move.joystickName != "new joystick")       //  在这里的名字new joystick 就是上面所说的很重要的名字，在上面图片中joystickName的你修改了什么名字，这里就要写你修改的好的名字（不然脚本不起作用）。
               {  
                         return;  
               }  

       float PositionX = move.joystickAxis.x;       //   获取摇杆偏移摇杆中心的x坐标
       float PositionY = move.joystickAxis.y;      //    获取摇杆偏移摇杆中心的y坐标

              if (PositionY != 0 || PositionX != 0)  
               {                //  设置控制角色或物体方块的朝向（当前坐标+摇杆偏移量）
                       transform.LookAt(new Vector3(transform.position.x + PositionX, transform.position.y, transform.position.z + PositionY));  
                                  //  移动角色或物体的位置（按其所朝向的位置移动）
                       transform.Translate(Vector3.forward * Time.deltaTime * 25);  
               }  
         } 
}  
```

　　
把此脚本放到需要用摇杆控制的物体上，即可实现摇杆控制物体移动。

## 五、实例

### 实例一
场景里放一个cube，当我用一根手指在屏幕上滑动的时候，我需要cube旋转；当我对它拖拽时，需要它跟着手指移动；当我用两根手指滑动时相机平面移动；当我双指向内捏或者向外拉时相机拉近或远。

![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg0NDA1MTQx?x-oss-process=image/format,png)
1.首先添加 easytouch游戏对象，它本身有许多设置选项，我大概过了一下，然后，啥也没记住。
这个简易demo里也不需要修改什么。
2.创建cube
3.创建脚本，并挂给cube
4.编写脚本

![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg0NDM0NDA2?x-oss-process=image/format,png)

这是easytouch中订阅事件的方法，EasyTouch下定义了各种类型的事件，我们只需要编写相应处理方法，然后+=订阅。在OnEnable中订阅，在OnDisable和OnDestroy中取消订阅。方法要传一个Gesture类型的参数，包含了手势的数据。

我的EasyTouchTest

```csharp
using System.Collections;  
using System.Collections.Generic;  
using UnityEngine;  
using HedgehogTeam.EasyTouch;  
using UnityEngine.UI;  
public class EasyTouchTest : MonoBehaviour {  
    public Button BtnReset;  
    // Use this for initialization  
    void Start () {  
          
    }  
      
    // Update is called once per frame  
    void Update () {  
          
    }  
  
    void OnEnable() {  
        EasyTouch.On_Swipe += On_Swipe;  
        EasyTouch.On_Drag += On_Drag;  
        EasyTouch.On_Swipe2Fingers += On_Swipe2Fingers;  
        EasyTouch.On_Pinch += On_Pinch;  
        BtnReset.onClick.AddListener(ResetScene);  
    }  
  
    void OnDisable() {  
        EasyTouch.On_Swipe -= On_Swipe;  
        EasyTouch.On_Drag -= On_Drag;  
        EasyTouch.On_Swipe2Fingers -= On_Swipe2Fingers;  
        EasyTouch.On_Pinch -= On_Pinch;  
        BtnReset.onClick.RemoveListener(ResetScene);  
    }  
  
    void OnDestroy() {  
        EasyTouch.On_Swipe -= On_Swipe;  
        EasyTouch.On_Drag -= On_Drag;  
        EasyTouch.On_Swipe2Fingers -= On_Swipe2Fingers;  
        EasyTouch.On_Pinch -= On_Pinch;  
        BtnReset.onClick.RemoveListener(ResetScene);  
    }  
  
    /// <summary>  
    /// 重置cube和相机  
    /// </summary>  
    void ResetScene() {  
        transform.position = Vector3.zero;  
        transform.rotation = Quaternion.Euler(Vector3.zero);  
        Camera.main.transform.position = new Vector3(0, 0, -10);  
    }  
  
    /// <summary>  
    /// 滑动使cube旋转  
    /// </summary>  
    /// <param name="ges"></param>  
    void On_Swipe(Gesture ges) {  
        Vector3 vec = new Vector3(ges.deltaPosition.y, ges.deltaPosition.x, 0);  
        transform.Rotate(vec ,Space.World);  
    }  
  
    /// <summary>  
    /// 拖拽移动cube  
    /// </summary>  
    /// <param name="ges"></param>  
    void On_Drag(Gesture ges) {  
        if (ges.pickedObject == gameObject) {  
            transform.position = ges.GetTouchToWorldPoint(10);//相机z=-10 cube 0  
        }  
    }  
  
    /// <summary>  
    /// 双指滑动 平面移动相机  
    /// </summary>  
    /// <param name="ges"></param>  
    void On_Swipe2Fingers(Gesture ges) {  
        Camera.main.transform.Translate(new Vector3(-ges.deltaPosition.x, -ges.deltaPosition.y, 0));  
    }  
  
    /// <summary>  
    /// 拉近拉远相机  
    /// </summary>  
    /// <param name="ges"></param>  
    void On_Pinch(Gesture ges) {  
        Camera.main.transform.Translate(new Vector3(0, 0, ges.deltaPinch));  
    }  
}  
```

参数还需要调整，但之前的小目标是实现了，因为容易一下子就把我的小Cube弄不见了，我就添加了一个复位按钮。

摇杆
剩下的我比较感兴趣的也就是摇杆了，毕竟这个东西挺常用，而且，如果你说要让我自己从头做一个，我还是觉得挺懵逼的···
右键EasyTouchControls->Joystick创建一个摇杆
常用的设置可能也就是Type，决定了摇杆是动态的还是静态的，静态就是坐标固定，动态的话当手指离开屏幕，摇杆会消失，手触摸的时候在手指触摸的坐标生成摇杆。
设为动态时可以选择摇杆区域全屏，半屏，还可以自定义区域。
摇杆的值

```csharp
Debug.Log(ETCInput.GetAxis("Horizontal")+","+ ETCInput.GetAxis("Vertical"));  
```



easytouch真的十分强大方便易上手，并且跟UGUI没有什么冲突。更多的功能只有在实际使用中去研究了。


### 实例二
摇杆控制人物移动

创建虚拟摇杆： 
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg0OTU4Nzgy?x-oss-process=image/format,png)
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1NDIxNTk3?x-oss-process=image/format,png)
好了，开始使用EasyTouch5实现角色的转向： 
如下设置虚拟摇杆参数： 
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1NjM3ODAy?x-oss-process=image/format,png)
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1NjQ4NzI5?x-oss-process=image/format,png)
实现角色转动，效果： 
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1NzAzNTg1?x-oss-process=image/format,png)
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1NzI4NTUx?x-oss-process=image/format,png)
以上是虚拟摇杆简单的应用，下面我们将实现角色第一人称的移动&转向： 
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1NzQzNzM4?x-oss-process=image/format,png)
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1ODAxMjYx?x-oss-process=image/format,png)
好了，第一人称视角的移动+转向完成！现在通过摇杆控制角色移动，相机会跟随在角色背后。

接着是第三人称视角： 
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDg1ODE1ODcz?x-oss-process=image/format,png)


只需要将Turn&Move 选项勾选上，即可控制人物移动&转向。

完成！哈哈，是不是好简单。完全不用接触代码层面，直接通过视图面板设置，这最适合初学者不过。但是没有接触过，或者只是使用过旧版的人可能就一头雾水了。



### 实例三
RPG类的游戏的摇杆控制人物移动
1、以下是EasyTouch插件的使用步骤：
1.import“EasyTouch”资源包

2.创建空物体，命名为EasyTouch(当然你也可以改成其他名字)

3.添加EasyTouch.cs脚本在刚刚创建的空物体（EasyTouch）上

4.选择改物体但不要将BroadcastMessages勾选

5.创建一个新的C#脚本，命名MyFirstTouch，然后添加以下方法

```csharp
void OnEnable(){    
EasyTouch.On_TouchStart += On_TouchStart;    
}    
// Unsubscribe    
void OnDisable(){    
EasyTouch.On_TouchStart -= On_TouchStart;    
}    
// Unsubscribe    
void OnDestroy(){    
EasyTouch.On_TouchStart -= On_TouchStart;    
}    
// Touch start event    
public void On_TouchStart(Gesture gesture){    
Debug.Log( "Touch in " + gesture.position);    
}    
```

6.再创建一个空物体，命名为Receiver

7.将MyFirstTouch脚本添加到空物体Receiver上

8.运行并且点击遥感，会发现控制台打印了当前按下的坐标

8、根据官方的这些提示，自己来做一个属于自己的人物遥感控制

1.导入EasyTouch3资源包
2.做好前期准备，包括人物模型、地形的创建
3.添加JoyStick实例：HedgehogTeam->EasyTouch->Extensions->Add a new Joystick。此时就会在左下角创建虚拟遥感实例          
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcxMTAzMDkwMTEwODky?x-oss-process=image/format,png)

9、创建脚本MoveController.cs用来接收遥感事件控制角色的移动    

```
using UnityEngine;    
using System.Collections;    
    
public class MoveController : MonoBehaviour {    
    
    void OnEnable()    
    {    
        EasyJoystick.On_JoystickMove += OnJoystickMove;    
        EasyJoystick.On_JoystickMoveEnd += OnJoystickMoveEnd;    
    }    
    
    
    //移动摇杆结束    
    void OnJoystickMoveEnd(MovingJoystick move)    
    {    
        //停止时，角色恢复idle    
        if (move.joystickName == "MoveJoystick")    
        {    
            animation.CrossFade("idle");    
        }    
    }    
    
    
    //移动摇杆中    
    void OnJoystickMove(MovingJoystick move)    
    {    
        if (move.joystickName != "MoveJoystick")    
        {    
            return;    
        }    
            
        //获取摇杆中心偏移的坐标    
        float joyPositionX = move.joystickAxis.x;    
        float joyPositionY = move.joystickAxis.y;    
    
    
        if (joyPositionY != 0 || joyPositionX != 0)    
        {    
            //设置角色的朝向（朝向当前坐标+摇杆偏移量）    
           transform.LookAt(new Vector3(transform.position.x + joyPositionX, transform.position.y, transform.position.z + joyPositionY));    
            //移动玩家的位置（按朝向位置移动）    
            transform.Translate(Vector3.forward * Time.deltaTime * 5);    
            //播放奔跑动画    
            animation.CrossFade("run");    
        }    
    }    
}    
```

10、创建点击按钮
点击HedgehogTeam->EasyTouch->Extensions->Create a new Button,会在屏幕右下角创建一个button
然后调节面板参数：

代码添加跟Unity中Button按钮添加方法类似。



### 最后附上研究的EasyTouch3.1.6 API
EasyTouch.On_TouchStart
函数作用：在点击的时候触发
使用例子：

```csharp
public void On_TouchStart(Gesture gesture)
{
		// Verification that the action on the object
		if (gesture.pickObject == gameObject)
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
	}
```
	
EasyTouch.On_TouchDown
函数作用：在按下的时候触发
使用例子：

```csharp
public void On_TouchDown(Gesture gesture)
{
		// Verification that the action on the object
		if (gesture.pickObject == gameObject)
			textMesh.text = "Down since :" + gesture.actionTime.ToString("f2");
	}
```
	

EasyTouch.On_TouchUp
函数作用：在松开的时候触发
使用例子：

```csharp
public void On_TouchUp(Gesture gesture)
{
		// Verification that the action on the object
		if (gesture.pickObject == gameObject)
		{
			gameObject.GetComponent<Renderer>().material.color = new Color( 1f,1f,1f);
			textMesh.text ="Touch Start/Up";
		}
}
```

EasyTouch.On_DoubleTap
函数作用：在双击的时候触发
使用例子：

```csharp
private void On_DoubleTap( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			
	 		gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```

EasyTouch.On_SimpleTap
函数作用：在普通的点击时候触发
使用例子：

```csharp
private void On_SimpleTap( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```

EasyTouch.On_LongTapStart
函数作用：在长点击的时候触发
使用例子：

```csharp
private void On_LongTapStart( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject==gameObject){
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```
	
EasyTouch.On_LongTap
函数作用：在长点击期间的时候触发
使用例子：

```csharp
private void On_LongTap( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject==gameObject){
			textMesh.text = gesture.actionTime.ToString("f2");
		}
	
	}
```

EasyTouch.On_LongTapEnd
函数作用：在长点击结束的时候触发
使用例子：

```csharp
private void On_LongTapEnd( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject==gameObject){
			gameObject.GetComponent<Renderer>().material.color = Color.white;
			textMesh.text="Long tap";
		}
	
	}
```

EasyTouch.On_Drag
函数作用：在拖拽期间的时候触发
使用例子：

```csharp
void On_Drag(Gesture gesture){
	
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			
			// the world coordinate from touch for z=5
			Vector3 position = gesture.GetTouchToWordlPoint(5);
			
			transform.position = position - deltaPosition;
			
			// Get the drag angle
			float angle = gesture.GetSwipeOrDragAngle();
			
			textMesh.text = gesture.swipe.ToString() + " / angle :" + angle.ToString("f2");
		}
	}
```

EasyTouch.On_DragStart
函数作用：在拖拽开始的时候触发
使用例子：

```csharp
void On_DragStart( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		
			// the world coordinate from touch for z=5
			Vector3 position = gesture.GetTouchToWordlPoint(5);
			
			
			deltaPosition = position - transform.position;
		}	
	}
```

EasyTouch.On_DragEnd
函数作用：在拖拽结束的时候触发
使用例子：

```csharp
void On_DragEnd(Gesture gesture){
	
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			transform.position= new Vector3(3f,1.8f,-5f);
			gameObject.GetComponent<Renderer>().material.color = Color.white;
			textMesh.text="Drag me";
		}
	}
```

EasyTouch.On_TouchStart2Fingers
函数作用：按住Ctrl然后点击的时候触发
使用例子：

```csharp
void On_TouchStart2Fingers( Gesture gesture){
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```
	
EasyTouch.On_TouchDown2Fingers
函数作用：按住Ctrl然后按下的时候触发
使用例子：

```csharp
void On_TouchDown2Fingers(Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			textMesh.text = "Down since :" + gesture.actionTime.ToString("f2");
		}
	}
```
	
EasyTouch.On_TouchUp2Fingers
函数作用：按住Ctrl然后松开的时候触发
使用例子：

```csharp
void On_TouchUp2Fingers( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			gameObject.GetComponent<Renderer>().material.color = Color.white;
			textMesh.text ="Touch Start/Up";
		}
	}
```

EasyTouch.On_Cancel2Fingers
函数作用：按住Ctrl然后取消的时候触发
使用例子：

```csharp
void On_Cancel2Fingers( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			gameObject.GetComponent<Renderer>().material.color = Color.white;
			textMesh.text ="Touch Start/Up";
		}
	}
```

EasyTouch.On_SimpleTap2Fingers
函数作用：按住Ctrl然后普通点击的时候触发
使用例子：

```csharp
void On_SimpleTap2Fingers( Gesture gesture){
		
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	

			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```

EasyTouch.On_DoubleTap2Fingers
函数作用：按住Ctrl然后双击的时候触发
使用例子：

```csharp
void On_DoubleTap2Fingers( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```

EasyTouch.On_LongTapStart2Fingers
函数作用：按住Ctrl然后长点击的时候触发
使用例子：

```csharp
void On_LongTapStart2Fingers( Gesture gesture){
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		}
	}
```

EasyTouch.On_LongTap2Fingers
函数作用：按住Ctrl然后长点击的期间的时候触发
使用例子：

```csharp
void On_LongTap2Fingers( Gesture gesture){
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){		
			textMesh.text = gesture.actionTime.ToString("f2");
		}
	}
```

EasyTouch.On_LongTapEnd2Fingers 
函数作用：按住Ctrl然后长点击结束的时候触发
使用例子：

```csharp
void On_LongTapEnd2Fingers( Gesture gesture){
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			gameObject.GetComponent<Renderer>().material.color = new Color(1f,1f,1f);
			textMesh.text="Long tap";
		}
	}
```

EasyTouch.On_Cancel2Fingers
函数作用：按住Ctrl然后长点击取消的时候触发
使用例子：

```csharp
void On_Cancel2Fingers(Gesture gesture){
		gameObject.GetComponent<Renderer>().material.color = new Color(1f,1f,1f);
		textMesh.text="Long tap";
	}
```

EasyTouch.On_PinchIn
函数作用：按住Next然后拖动的时候触发，缩小
使用例子：

```csharp
// At the 2 fingers touch beginning
	private void On_TouchStart2Fingers( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){		
			// disable twist gesture recognize for a real pinch end
			EasyTouch.SetEnableTwist( false);
			EasyTouch.SetEnablePinch( true);
		}
	}
private void On_PinchIn(Gesture gesture){
	
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			
			float zoom = Time.deltaTime * gesture.deltaPinch;
		
			Vector3 scale = transform.localScale ;
			transform.localScale = new Vector3( scale.x - zoom, scale.y -zoom, scale.z-zoom);
			
			textMesh.text = "Delta pinch : " + gesture.deltaPinch.ToString();
		}
		
	}
```
	
EasyTouch.On_PinchOut
函数作用：按住Next然后拖动的时候触发，扩大
使用例子：

```csharp
private void On_PinchOut(Gesture gesture){
	
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			float zoom = Time.deltaTime * gesture.deltaPinch;
		
			Vector3  scale = transform.localScale ;
			transform.localScale = new Vector3( scale.x + zoom, scale.y +zoom,scale.z+zoom);
			
			textMesh.text = "Delta pinch : " + gesture.deltaPinch.ToString();
		}
	}
```
	
EasyTouch.On_PinchEnd
函数作用：按住Next然后拖动结束的时候触发
使用例子：

```csharp
private void On_PinchEnd(Gesture gesture){
		
		if (gesture.pickObject == gameObject){
			transform.localScale =new Vector3(1.7f,1.7f,1.7f);
			EasyTouch.SetEnableTwist( true);
			textMesh.text="Pinch me";
		}
		
	}
```

EasyTouch.On_Twist
函数作用：按住Next然后旋转的时候触发
使用例子：

```csharp
// At the 2 fingers touch beginning
	void On_TouchStart2Fingers( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){			
			EasyTouch.SetEnablePinch( false);
			EasyTouch.SetEnableTwist( true);
		}
	}
	
	// during the txist
	void On_Twist( Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			transform.Rotate( new Vector3(0,0,gesture.twistAngle));
			textMesh.text = "Delta angle : " + gesture.twistAngle.ToString();
		}
	}
```

EasyTouch.On_TwistEnd
函数作用：按住Next然后旋转结束的时候触发
使用例子：

```csharp
void On_TwistEnd( Gesture gesture){

		// Verification that the action on the object
		if (gesture.pickObject == gameObject){
			EasyTouch.SetEnablePinch( true);
			transform.rotation = Quaternion.identity;
			textMesh.text ="Twist me";
		}
	}

```

EasyTouch.On_Drag2Fingers
函数作用：按住Ctrl然后拖动的时候触发
使用例子：

```csharp
// At the drag beginning
	void On_DragStart2Fingers(Gesture gesture){

		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			gameObject.GetComponent<Renderer>().material.color = new Color( Random.Range(0.0f,1.0f),  Random.Range(0.0f,1.0f), Random.Range(0.0f,1.0f));
		
			Vector3 position =  gesture.GetTouchToWordlPoint(  5);
			deltaPosition = position - transform.position;
		}
	}
	
	// During the drag
	void On_Drag2Fingers(Gesture gesture){

		// Verification that the action on the object
		if (gesture.pickObject == gameObject){	
			Vector3 position = gesture.GetTouchToWordlPoint(  5);
			
			transform.position = position - deltaPosition;
			
			float angles =  gesture.GetSwipeOrDragAngle(); 
			
			textMesh.text = gesture.swipe.ToString() + " / angle :" + angles.ToString("f2");
		}
	}
```
	
EasyTouch.On_DragEnd2Fingers
函数作用：按住Ctrl然后拖动结束的时候触发
使用例子：

```csharp
// At the drag end
	void On_DragEnd2Fingers(Gesture gesture){
		
		// Verification that the action on the object
		if (gesture.pickObject == gameObject){			
			transform.position=new Vector3(2.5f,-0.5f,-5f);
			gameObject.GetComponent<Renderer>().material.color = new Color(1f,1f,1f);
			textMesh.text="Drag me";
		}
	}
```

Joystick.On_Manual
函数作用：手动摇杆，参数是Vecotr2
使用例子：

```csharp
Joystick.On_Manual(new Vector2(Input.GetAxis ("Horizontal"), Input.GetAxis("Vertical")));
```

EasyJoystick.On_JoystickMove
函数作用：移动的时候触发
使用例子：

```csharp
void On_JoystickMove( MovingJoystick move){
	
		float angle = move.Axis2Angle(true);
		transform.rotation  = Quaternion.Euler( new Vector3(0,angle,0));
		transform.Translate( Vector3.forward * move.joystickValue.magnitude * Time.deltaTime);	
		
		model.GetComponent<Animation>().CrossFade("Run");

	}
```

EasyJoystick.On_JoystickMoveEnd
函数作用：移动结束的时候触发
使用例子：

```csharp
void On_JoystickMoveEnd (MovingJoystick move)
	{
		model.GetComponent<Animation>().CrossFade("idle");
	}
```

## 六、EasyTouch计算摇杆旋转角度以及摇杆八方向控制角色


在写第三人称控制的时候，一开始在电脑测试是用WASD控制角色
后来需要发布到手机上，于是就加了一个摇杆
键盘控制角色的代码已经写好了，角色八方向移动

### 传统控制思路

```csharp
 //当摇杆处于移动状态时，角色开始奔跑
  void OnJoystickMove(MovingJoystick move)
  {
    if (move.joystickName != "EasyJoystick")
    {
       return;
    }
   //获取摇杆偏移量
   float joyPositionX = move.joystickAxis.x;
   float joyPositionY = move.joystickAxis.y;
   if (joyPositionY != 0 || joyPositionX != 0)
   {
      //设置角色的朝向（朝向当前坐标+摇杆偏移量）
      transform.LookAt(new Vector3(transform.position.x + joyPositionX, transform.position.y, transform.position.z + joyPositionY));
       //移动玩家的位置（按朝向位置移动）
      transform.Translate(Vector3.forward * Time.deltaTime * 7.5F);
      //播放奔跑动画
       animation.CrossFade("Run");
     }
  }
```
### 控制摇杆角度
如果要按照摇杆传统思路控制角色，在重新写控制角色代码的话非常麻烦，所以我就通过计算摇杆旋转角度来判断当前摇杆处于哪个方向
ok，现在我们开始来敲代码
首先，我们来调试观察一下摇杆的x轴、y轴的返回值
//移动摇杆中  

```csharp
void OnJoystickMove(MovingJoystick move)
{
      Debug.Log(move.joystickAxis.x + "," + move.joystickAxis.y);
}
```
调试结果为：
左：x = -1，y = 0；顺时针旋转X逐渐变大，Y逐渐变大
上：x = 0，y = 1；顺时针旋转X逐渐变大，Y逐渐变小
右：x = 1，y = 0；顺时针旋转X逐渐变小，Y逐渐变小
下：x = 0，y = -1；顺时针旋转X逐渐变小，Y逐渐变大
我们把摇杆底图看成是两个半圆，上半圆和下半圆
![在这里插入图片描述](https://img-blog.csdn.net/20151223160823558?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
那么：
X轴移动到左边时，X = -1；X轴移动到右边时：X = 1；X轴从左转到右旋转了180度
Y轴移动到左边时，Y = 0；Y轴移动到右边时：Y = 0；Y轴从左转到右旋转了180度
你如果直接看我的调试结果肯定有点晕，建议边调试边参考我的调试结果，这样才能理解
如果我们要计算当前摇杆在左上角旋转的度数怎么计算呢？
读过小学的人都可以做，只是看见摇杆返回的-1和0脑袋被绕迷糊了，我也一样，弄了好半天才弄好

当摇杆移动到左时，为0度、360度(因为360度为一圈，已经绕回远点了)
当摇杆移动到上时，为90度
当摇杆移动到右时，为180度
当摇杆移动到下时，为270度

既然知道是多少度这就好办多了
得出公式：
当X轴在右时为1，也就是X轴为180度，则：1 * 90 + 90 = 180
当前X轴旋转角度为：X轴返回值 * 90度 + 90度

你以为这就完事了吗？还高兴得太早，用这个公式计算只能得到上半圆的旋转角度
现在我们要获取下半圆旋转角度，然后用上半圆旋转角度 + 下半圆旋转角度 = 当前旋转角度
当摇杆移动到下半圆时我们怎么计算旋转角度呢？
我们已经知道Y轴在左边为0，在右边为0，在下边为-1，继续用计算X轴的公式

Y左：0 * 90 + 90 = 90
Y上：1 * 90 + 90 = 180
Y下：-1 * 90 + 90 = 0
Y右：0 * 90 + 90 = 90
X左：-1 * 90 + 90 = 0
X上：0 * 90 + 90 = 90
X下：0 * 90 + 90 = 90
X右：1 * 90 + 90 = 180

从计算结果中可以得出结论
当Y轴小于90度时，摇杆就处于下半圆
当Y轴小于90度时且X小于90度时为左下：270度 + Y轴旋转角度
当Y轴小于90度时且X大于90度时为右下：180度 + Y轴旋转角度
思路搞定了，开始敲代码，代码不多，我直接贴上来了，看完上诉文字相信你已经知道这些代码是怎么回事了

```csharp
/// 计算摇杆角度 <summary>
/// 计算摇杆角度
/// </summary>
/// <param name="_joyPositionX">摇杆X轴</param>
/// <param name="_joyPositionY">摇杆Y轴</param>
/// <returns>返回当前摇杆旋转多少度</returns>
private float CalculaAngle(float _joyPositionX, float _joyPositionY)
{
   float currentAngleX = _joyPositionX * 90f + 90f;//X轴 当前角度
   float currentAngleY = _joyPositionY * 90f + 90f;//Y轴 当前角度
   //下半圆
   if (currentAngleY < 90f)
   {
        if (currentAngleX < 90f)
        {
             return 270f + currentAngleY;
        }
        else if (currentAngleX > 90f)
        {
              return 180f + (90f - currentAngleY);
        }
     }
     return currentAngleX;
}
```
ok，现在知道当前摇杆旋转了多少度，我们可以轻松的用角度来判断当前移动方向了

用键盘控制时：
A = 左
WA = 左上
W = 上
WD = 右上
D = 右
SD = 右下
S = 下
SA = 左下

当摇杆角度为0度，往左
当摇杆角度为90度，往上
当摇杆角度为180度，往右
那我们肯定不能这样写啊，你能确定玩家操作摇杆那么精确啊？
因为我这里控制角色是八方向，所以：360 / 8 = 45
每个方向有45度可触发，那么得出以下解决方案：
上：当前角度 <= 90 + 45 / 2 = 112.5 && 当前角度 >= 90 - 45 / 2 = 67.5
如法炮制，得出以下代码：

```csharp
float currentAngle = CalculaAngle(joyPositionX, joyPositionY);

if (currentAngle <= 22.5f && currentAngle >= 0f || currentAngle <= 360f && currentAngle >= 337.5f)//0;左
    CurrentDire = "A";
else if (currentAngle <= 67.5f && currentAngle >= 22.5f)//45;左上
    CurrentDire = "WA";
else if (currentAngle <= 112.5f && currentAngle >= 67.5f)//90;上
    CurrentDire = "W";
else if (currentAngle <= 157.5f && currentAngle >= 112.5f)//135;右上
    CurrentDire = "WD";
else if (currentAngle <= 202.5f && currentAngle >= 157.5f)//180;右
    CurrentDire = "D";
else if (currentAngle <= 247.5f && currentAngle >= 202.5f)//225;右下
    CurrentDire = "SD";
else if (currentAngle <= 292.5f && currentAngle >= 247.5f)//270;下
    CurrentDire = "S";
else if (currentAngle <= 337.5f && currentAngle >= 292.5f)//315;左下
    CurrentDire = "SA";
```

大功告成，赶紧发布到手机上跑一下试试，这就是我想要的摇杆八方向操作效果
