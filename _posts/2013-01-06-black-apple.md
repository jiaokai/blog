---
layout: post
title: 我的黑苹果
categories: [Mac]
tags: [Mac]
---

## 配置

- CPU: i3 2125
- 内存：三星(SAMSUNG) 黑武士DDR3 1600 8G(4G×2条)
- 主板：华擎H77M-ITX
- 显卡：CPU核显 HD3000
- 硬盘：三星SSD 830 Series SATA III（MZ-7PC128B/WW）

## 提取dsdt

在windows或者linux下，使用dsdt editor，提取这块主板的dsdt，dsdt editor这个神器需要java。

linux下涉及一些权限问题，请使用一下命令：

{% highlight bash %}
    sudo java -jar dsdteditor.jar
{% endhighlight %}

Windows 下使用右键，管理员运行即可。

## 修改dsdt

- 修正所有错误，dsdt的错误修正可以Google之。
- 添加网卡内置代码
- 添加HD3000驱动代码（对于7系列主板，HD3000的驱动要复杂一点）
- 添加声卡代码
- 修正所有警告，无非就是一些没有返回值的函数

## 安装驱动和变色龙引导

## 完成

三言两句就讲完了，玩黑苹果是个折腾的过程，当你折腾一边回来之后，感觉其实很简单。就我自己的理解，苹果并没有
故意的不让mac系统装到普通PC上，只是mac在开发的时候主要照顾了苹果自己的硬件，而黑苹果就是把自己的普通PC尽量
地模仿成白苹果一样，最方便的方法就是通过dsdt伪装。

另：其实这款主板不用dsdt一样可以安装并进入系统，但是HD3000只能使用dsdt来驱动。如果你有HD4000，那么完全可以
抛开dsdt。

