---
layout: post
title: Python virtualenv
categories: [Python]
tags: [Python]
---

比如说，我以前做过几个项目用的是 django 1.3 版本，现在又有一个新的项目，准备尝尝鲜，使用django 1.5。如果不实用`virtualenv`，那正常的做法就是将系统中的 django 1.3 删除，然后安上 django 1.5。以前的项目虽然稳定，但有时候还要维护，我不可能将它们都升级到 django 1.5。那么我如何在django 1.3版本和1.5版本之间方便的切换呢。

更通用的问题是：我如何为我所有的Python项目，设置单独的、适用于此项目的、与其他项目不冲突的开发环境呢？

解决方案就是：`virtualenv`，它的作用就是为每一个项目设置单独的与其他项目不会冲突的环境。

## 安装

{% highlight bash %}
$ pip install virtualenv
{% endhighlight %}

## 使用

在开发目录下：

{% highlight bash %}
$ virtualenv ENV
New python executable in venv/bin/python
Installing distribute............done.

$ . ENV/bin/activate
or
$ source ENV/bin/activate

# 然后安装此项目使用的依赖
$ pip install django==1.5
$ pip install DjangoUeditor
{% endhighlight %}

## 引用

- [virtualenv](http://www.virtualenv.org/en/latest/)
