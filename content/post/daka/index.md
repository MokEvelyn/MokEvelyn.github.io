---
title: 利用锁屏启动自动完成粤省事场所码打卡
date: 2022-10-11
tags:
- 自动化
- 快捷指令
- 小程序
categories: 
- OpenSource
thumbnail: "cover.png"
url: "daka"
---



锁屏启动App是一款基于iOS16系统的快捷指令软件，可以通过简单设置一键打开健康码/核酸码/行程码/等日常经常需要用到的二维码，并且通过小组件形式可以使用户在锁屏状态下快速亮码。

但除此之外，还可以通过这样一款小巧的App实现一键打卡场所码的功能，避免每次进出常去场所时打卡的麻烦。

<!--more-->



# 项目目的

通过外部App唤起微信小程序，并实现一键自动打卡场所码的目的。



# 配置步骤

### 资料准备

1.拍下经常出入的场所的场所码作为备用，比如小区、公司写字楼、上下班需要进入的地铁站、经常去的商圈等



2.打开已经注册的公众号后台（公众号注册和绑定可以在网上看一下教程），并点击<font color=#2596be>首页—新的创作—图文消息</font>

<img src="image-20221015152819425.png" alt="image-20221015152819425" style="zoom:67%;" />



3.在图文消息创作页面顶端，点击<font color=#2596be>小程序</font>

![image-20221015152924620](/Users/mokunyang/Desktop/daka/image-20221015152924620.png)



4.选择小程序页面内输入<font color=#2596be>粤省事</font>，点击进入下一步

<img src="/Users/mokunyang/Desktop/daka/image-20221015153713625.png" alt="image-20221015153713625" style="zoom:67%;" />



5.在填写详细信息页面中，将鼠标光标置于小程序路径框下方的<font color=#2596be>获取更多页面途径</font>位置，并在右侧弹出框中输入<font color=#2596be>需要进行场所码打卡的微信号</font>后，点击<font color=#2596be>开启</font>按钮

<img src="/Users/mokunyang/Desktop/daka/image-20221015153844834.png" alt="image-20221015153844834" style="zoom:67%;" />



6.打开微信扫一扫，扫描第一步中拍下的需要打卡的场所码，点击右上角<font color=#2596be>三个点</font>，在下方弹出框中点击<font color=#2596be>复制页面路径</font>

<img src="/Users/mokunyang/Desktop/daka/image-20221015154459615.png" alt="image-20221015154459615" style="zoom:33%;" />



7.点击下方弹出框中<font color=#2596be>粤省事</font>，点击<font color=#2596be>更多资料</font>，复制<font color=#2596be>账号原始ID</font>

<img src="/Users/mokunyang/Desktop/daka/image-20221015154944528.png" alt="image-20221015154944528" style="zoom:33%;" />



<img src="/Users/mokunyang/Desktop/daka/image-20221015155101079.png" alt="image-20221015155101079" style="zoom:33%;" />



<img src="/Users/mokunyang/Desktop/daka/image-20221015155150912.png" alt="image-20221015155150912" style="zoom:33%;" />



### 软件安装

在App Store中搜索<font color=#2596be>锁屏启动</font>App，下载安装



### 快捷指令设置

1.在App内<font color=#2596be>锁屏页面</font>，点击待设置项右侧<font color=#2596be>三个点</font>，点击弹出框中<font color=#2596be>编辑</font>

<img src="/Users/mokunyang/Desktop/daka/image-20221015155649775.png" alt="image-20221015155649775" style="zoom:33%;" />



2.在编辑启动项页面中点击<font color=#2596be>自定义</font>，并将之前复制下来的小程序账号原始ID和场所码页面路径复制到下面对应位置中，将完整链接粘贴到<font color=#2596be>URL Scheme框</font>内，点击保存并测试运行，场所码即可一键自动打卡

<font color=#2596be>`weixin://?userName=小程序账号原始ID&path=页面路路径`</font>

<img src="/Users/mokunyang/Desktop/daka/image-20221015160005159.png" alt="image-20221015160005159" style="zoom:33%;" />



3.重复上述操作，可以将常用的场所码都设置为<font color=#2596be>桌面小组件</font>，在需要时即可一键打卡，避免频繁的扫码和等待亮码