---
layout: post
title: Centos 6.4 Minimal 安装记录
categories: [CLI]
tags: [CLI, Linux, Centos]
---

## 1. 制作安装u盘

UltraISO写入完成后，只保留「images」和「isolinux」两个文件夹，其余全部删除，然后复制CentOS-6.4-x86_64-minimal.iso到u盘根目录。

## 2. 安装RPMForge软件库

    # 导入 rpmforge 的GPG密钥
    rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt
    # 安装
    yum install http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
    # 安装软件
    yum install htop
    #yum install phpmyadmin
    yum -y install gcc gdb make man vim wget
    yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel

## 3. 关闭 SELINUX

    vim /etc/selinux/config
    # SELINUX=enforcing          # 注释掉
    # SELINUXTYPE=targeted    # 注释掉
    SELINUX=disabled               # 增加
    shutdown -r now  # 重启系统

## 4. nginx

nginx 官方有源

    wget http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6.0.el6.ngx.noarch.rpm
    rpm -ivh nginx-release-centos-6.0.el6.ngx.noarch.rpm
    yum install nginx
    chkconfig nginx on

nginx 默认目录：

    whereis nginx
    nginx: /usr/sbin/nginx /etc/nginx /usr/share/nginx

1. 配置所在目录：/etc/nginx/
2. PID目录：/var/run/nginx.pid
3. 错误日志：/var/log/nginx/error.log
4. 访问日志：/var/log/nginx/access.log
5. 默认站点目录：/usr/share/nginx/html

常用命令：
 
    # 启动nginx
    nginx
    # 重启nginx
    killall -HUP nginx
    # 测试nginx配置
    nginx -t


## 5. Mysql

    yum install mysql mysql-server
    chkconfig mysqld on 或者 chkconfig --levels 235 mysqld on
    cp /usr/share/mysql/my-medium.cnf /etc/my.cnf
    /etc/init.d/mysqld start

    # 设置mysql root 密码
    mysql_secure_installation

    # 常用命令
    /etc/init.d/mysqld start
    /etc/init.d/mysqld stop
    service mysqld restart

## 6. php

    yum install php
    yum install php-mysql php-gd libjpeg* php-imap php-ldap php-pear php-xml php-xmlrppc php-mbstring php-mcrypt php-bcmatch php-mhash libmcrypt libmcrypt-devel php-fpm
    chkconfig php-fpm on
    /etc/init.d/mysqld restart
    /etc/init.d/nginx restart
    /etc/init.d/php-fpm start

## 7. 定时校正服务器时间

    yum install ntp
    crontab -e
    * 4 * * * ntpdate ntp.api.bz

 ntp.api.bz 是一组NTP服务器集群，目前有6台服务器。这项服务是api.bz继移动飞信免费短信发送接口之后的第二项免费服务

## 8. 关闭 ipv6

from: [http://hi.baidu.com/404656204/item/848f29d2f9231014d68ed0db](http://hi.baidu.com/404656204/item/848f29d2f9231014d68ed0db)

    # 查看内核模块加载信息：
    lsmod | grep ipv6

关闭：

    # 一. 修改/etc/sysconfig/network，追加：
    NETWORKING_IPV6=no
    # 二. 修改/etc/hosts,把ipv6的那句本地主机名解析的也注释掉：
    #::1   localhost localhost6 localhost6.localdomain6
    # 三. 让系统不加载ipv6相关模块，这需要修改modprobe相关设定文件，为了管理方便，我们新建设定文件/etc/modprobe.d/ipv6off.conf(名字随便起)（RHEL6.0之后没有了/etc/modprobe.conf这个文件），内容如下，三种方式，总有一款适合你：
    alias net-pf-10 off
    options ipv6 disable=1
    # 或者
    install ipv6 /bin/true
    # 或者
    install ipv6 /sbin/modprobe -n -i ipv6

注意，如果你使用了网卡绑定(bond)技术，而且不希望用ipv6，那么你使用第一种，否则系统启动时，bonding模块可能会加载失败。

4.重启系统，然后确认：

    [root@test ~]# lsmod | grep -i ipv6
    [root@test ~]# ifconfig | grep -i inet6

如果上述2个命令执行的结果没有任何显示，那么说明ipv6已经被完全禁止了。

后记：

在第三步不加载ipv6模块的方法里，可能有人会有类似这样的设置方法：

    alias net-pf-10 off
    alias ipv6 off
    options ipv6 disable=1

虽然这样在系统重启后，ipv6的确没被加载，但是因为第二句，在有的版本的系统里，当我们重启网络的时候，会出现如下错误：

    FATAL: Module off not found.

我估计大家都不希望在启动过程中看到FATAL这样的错误信息，所以我就采用正文里所设置的方法。

## 9. noatime, nodiratime

`/etc/fstab` 文件中

![fstab](/media/images/centos-fstab.png)

## 10. file limit ulimit

`/etc/rc.local` 添加一行：

    ulimit -SHn 102400

`/etc/security/limits.conf` 中添加：

    *          soft     nofile     65535
    *          hard     nofile     65535

## 11. centos 运行级别

     在 `/etc/inittab` 中

## 12. 设置服务

 from: http://www.lnton.com/index.php/archives/938

## 13. 优化内核

在 `/etc/sysctl.conf` 插入以下：

    net.ipv4.tcp_max_syn_backlog = 65536
    net.core.netdev_max_backlog =  32768
    net.core.somaxconn = 32768
    net.core.wmem_default = 8388608
    net.core.rmem_default = 8388608
    net.core.rmem_max = 16777216
    net.core.wmem_max = 16777216
    net.ipv4.tcp_timestamps = 0
    net.ipv4.tcp_synack_retries = 2
    net.ipv4.tcp_syn_retries = 2
    net.ipv4.tcp_tw_recycle = 1
    #net.ipv4.tcp_tw_len = 1
    net.ipv4.tcp_tw_reuse = 1
    net.ipv4.tcp_syncookies = 1
    net.ipv4.tcp_mem = 94500000 915000000 927000000
    net.ipv4.tcp_max_orphans = 3276800
    net.ipv4.tcp_fin_timeout = 30
    net.ipv4.tcp_keepalive_time = 120
    net.ipv4.ip_local_port_range = 1024 65535

执行以下命令使内核配置立马生效：

    /sbin/sysctl -p

## 14. 禁止IP伪装

     vim /etc/host.conf
     在里面加上：
     nospoof on

## 15. 安装 nethogs

    wget http://dl.fedoraproject.org/pub/epel/6/x86_64/nethogs-0.8.0-1.el6.x86_64.rpm
    rpm -ivh nethogs-0.8.0-1.el6.x86_64.rpm

运行：

`nethogs -d 3 eth0` #数据刷新时间为3秒

nethogs运行时的控制键：

`q` 退出
`m` 切换显示总流量或即时流量，总流量可切换三种显示模式B,KB,MB

## 16. iptables 配置

    sudo iptables -I INPUT -p tcp --dport 80 -j ACCEPT
    # 保存配置表
    sudo /etc/init.d/iptables save
    # 查看打开的端口
    sudo /etc/init.d/iptables status
    # 关闭防火墙
    sudo /etc/init.d/iptables stop

## 17. 其他参考

[1]: http://www.linuxde.net/2011/12/5756.html

