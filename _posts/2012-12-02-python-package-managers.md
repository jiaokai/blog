---
layout: post
title: Python 包管理工具关系与用法
categories: [Python]
tags: [Python, Code]
---

![Past-Present-Future](/media/images/python-package-managers-1.jpg)

## distutils

`distutils` 是Python 自带的基本安装工具，适用于非常简单的场景：

- 为项目创建 `setup.py` 脚本
- 执行 `setup.py install` 进行安装

## setuptools

针对 `distutils` 做了大量扩展，尤其是加入了`包依赖机制`。在部分Python子社区已成为事实的标准；

## distribute

由于 `setuptools` 开发进度缓慢，基本已经停止维护，不支持Python3，代码混乱，一帮程序员另起炉灶，
重构代码，增加功能，希望能够取代 `setuptools` 并被接纳为官方标准库，他们非常努力，在很短的时间
便让社区接受了 `distribute`。

## easy_install

`setuptools` 和 `distribute` 自带的安装脚本，也就是一旦 `setuptools` 或 `distribute` 安装完毕，
`easy_install`也便可用。

最大的特点是自动查找 Python 官方维护的包源 `PyPI`，安装第三方 Python 包非常方便:

    # 自动从 PyPI 查找/下载/安装指定的包
    easy_install [PACKAGE_NAME]

`setuptools` / `distribute` 都只是扩展了 distutils；

## pip

`pip` 的目标非常明确 – 取代 `easy_install`。

`easy_install` 有很多不足: 

- 安装事务是非原子操作
- 只支持 `svn`
- 没有提供卸载命令
- 安装一系列包时需要写脚本

`pip` 解决了以上问题，已俨然成为新的事实标准，`virtualenv` 与它已经成为一对好搭档：

    pip install [PACKAGE_NAME]
    pip uninstall [PACKAGE_NAME]

`pip` 支持从任意能够通过 VCS 或浏览器访问到的地址安装 Python 包

## distutils2

`setuptools` 和 `distribute` 的诞生是因为 `distutils` 的不济，进而导致目前分化的状况。
而 `Guido` 并未接纳 `distribute` 为官方标准，并说明了原因。开发者在失落之余明确了新的方向和任务 – `distutils2`，
它将成为 Python3.3 的标准库 `packaging` ，并在其它版本中以 `distutils2` 的身份出现，换句话说，
它和 `pip` 将联手结束目前混乱的状况;


## 引用

- [Python 包工具之间的关系](http://blog.yangyubo.com/2012/07/27/python-packaging/)
- [Why use pip over easy_install?](http://stackoverflow.com/questions/3220404/why-use-pip-over-easy-install)

-- 未完成 --
