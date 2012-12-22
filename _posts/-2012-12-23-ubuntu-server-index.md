---
layout: post
title: Ubuntu Server 安装配置
categories: [Linux]
tags: [Linux, Server]
---

- LVM
- 软件包管理工具
    - aptitude
- 系统监视分析工具
    - htop
    - [dstat](http://dag.wieers.com/home-made/dstat/)
    - nethogs
    - netstat
- php/nginx/apache
    - memcached
- 服务器压力测试
    - ab
    - httperf



### aptitude

aptitude update 更新可用的包列表
aptitude upgrade 升级可用的包
aptitude dist-upgrade 将系统升级到新的发行版
aptitude install pkgname 安装包
aptitude remove pkgname 删除包
aptitude purge pkgname 删除包及其配置文件
aptitude search string 搜索包
aptitude show pkgname 显示包的详细信息
aptitude clean 删除下载的包文件
aptitude autoclean 仅删除过期的包文件