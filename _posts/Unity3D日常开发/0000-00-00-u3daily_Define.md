---
layout:   blog
istop:	  true
u3daily:  true
category: Unity3D-Daily
title:    Unity3D 多平台_预编译相关宏定义
date:     2020-08-21 20:09:00
background-image: http://cdn.qq764424567.top/define0.png
tags:
- Unity3D
- Unity3D日常开发
---


## 一、平台定义

<table width="100%" style="border:0px; border-collapse:collapse; font-size:13px; color:rgb(68,68,68); font-family:Helvetica,Arial,sans-serif; line-height:17px">
<tbody>
<tr class="tableheader" style="visibility:hidden">
<td class="prop" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px; width:188px; visibility:hidden; height:1px">
&nbsp;</td>
<td class="function" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px; width:752px; visibility:hidden; height:1px">
&nbsp;</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_EDITOR</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
编辑器调用。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_STANDALONE_OSX</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
专门为Mac OS（包括<span style="color:rgb(34,34,34); font-family:arial; font-size:13px; text-align:justify">Universal</span>，PPC和Intel<span style="color:rgb(34,34,34); font-family:arial; font-size:13px; text-align:justify">architectures</span>）平台的定义。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_DASHBOARD_WIDGET</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span style="color:rgb(68,68,68); font-family:Helvetica,Arial,sans-serif; line-height:17px">Mac OS&nbsp;</span>Dashboard widget (<span style="color:rgb(68,68,68); font-family:Helvetica,Arial,sans-serif; line-height:17px">Mac OS仪表板小部件)</span>。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_STANDALONE_WIN</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
Windows。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_STANDALONE_LINUX</span></td>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
Linux的独立的应用程序。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_STANDALONE</span></td>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
独立的平台（Mac，Windows或Linux）。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_WEBPLAYER</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
网页播放器（包括Windows和Mac Web播放器可执行文件）。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_WII</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
Wii游戏机平台。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_IPHONE</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
iPhone平台。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_ANDROID</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
Android平台。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_PS3</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
PlayStation 3。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_XBOX360</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
Xbox 360。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_NACL</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
谷歌原生客户端（使用这个必须另外使用<span class="doc-prop" style="font-weight:bold">UNITY_WEBPLAYER</span>）。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_FLASH</span></td>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
Adobe Flash。</td>
</tr>
</tbody>
</table>
</div>
<div>
<p><strong><span style="font-size:14px">也可以判断Unity版本，目前支持的版本</span></strong></p>
<p><strong><span style="font-size:14px"></span></strong>
<table width="100%" style="border:0px; border-collapse:collapse; font-size:13px; color:rgb(68,68,68); font-family:Helvetica,Arial,sans-serif; line-height:17px">
<tbody>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_2_6</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 2.6。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_2_6_1</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义的特定版本1的主要版本2.6。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_0</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 3.0。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_0_0</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义的特定版本的Unity 3.0 0。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_1</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 3.1。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_2</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 3.2。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_3</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 3.3。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_4</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 3.4。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_3_5</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 3.5。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_4_0</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 4.0。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_4_0_1</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
主要版本4.0.1统一的平台定义。</td>
</tr>
<tr>
<td align="left" style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
<span class="doc-prop" style="font-weight:bold">UNITY_4_1</span></td>
<td style="font-family:Helvetica,Arial,sans-serif; vertical-align:top; padding:0px">
平台定义为主要版本的Unity 4.1。</td>
</tr>
</tbody>
</table>

## 二、运行平台

```csharp
//获得当前运行平台
Debug.Log(&quot;plat = &quot; + Application.platform);</pre>
```


//可以获取到的平台类型
```csharp
	public enum RuntimePlatform
    {
        OSXEditor = 0,
        OSXPlayer = 1,
        WindowsPlayer = 2,
        OSXWebPlayer = 3,
        OSXDashboardPlayer = 4,
        WindowsWebPlayer = 5,
        WiiPlayer = 6,
        WindowsEditor = 7,
        IPhonePlayer = 8,
        PS3 = 9,
        XBOX360 = 10,
        Android = 11,
        NaCl = 12,
        LinuxPlayer = 13,
        FlashPlayer = 15,
    }
 ```
