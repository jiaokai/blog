---
layout: post
title: Dz设置空间主题回复隐私
categories: [Discuz]
tags: [Discuz, php]
---

Discuz X3.0 不能让用户自己设置在自己的空间内隐藏主题回复，不过通过修改源代码，仅需4步，不需要修改数据库，即可添加这项功能。

## 1. 修改语言模板

在 `/source/language/home/lang_template.php` 文件中，添加：

    'jiao_threadandreply' => '主题/回复',
    'jiao_public' => '公开',
    'jiao_privacy' => '保密',

## 2. 修改隐私设置模板

在 `/template/default/home/spacecp_privacy.htm` 中，122行左右，添加：

    <tr>
        <th>{lang jiao_threadandreply}</th>
        <td>
            <select name='privacy[view][thread]'>
                <option value="0"$sels[view][thread][0]>{lang jiao_public}</option>
                <option value="2"$sels[view][thread][2]>{lang jiao_privacy}</option>
            </select>
        </td>
    </tr>

## 3. 修改隐私设置提交函数

在 `/source/include/spacecp/spacecp_privacy.php` 文件中：

    # 将 21 行左右：
    $viewtype = array('index', 'friend', 'wall', 'doing', 'blog', 'album', 'share', 'home', 'videoviewphoto');
    # 修改为：
    $viewtype = array('index', 'friend', 'wall', 'doing', 'blog', 'album', 'share', 'home', 'videoviewphoto', 'thread');

## 4. 修改空间主题显示页面

在 `/source/include/space/space_thread.php` 中，24行左右添加：

    $jiao_dd = $space['privacy']['view']['thread'];
    if( ($space['uid'] != $_G['uid']) && ($jiao_dd == 2)  && ($_G['adminid'] != 1)){
        $_G['privacy'] = 1;
        require_once libfile('space/profile', 'include');
        include template('home/space_privacy');
    } else {

在这个文件倒数第二行添加一个 `}` 号。

这样在个人「隐私筛选」中，即可设置空间内主题回复是否隐藏。

![隐藏主题回复](/media/images/dz-privacy.jpg)
