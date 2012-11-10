---
layout: post
title: Vim Plugin：vim-surround
categories: [vim]
tags: [vim]
---

可以方便的对括号、引用、XML标签等等进行删除、修改、添加等操作。

链接：[github](https://github.com/tpope/vim-surround), [vim.org](http://www.vim.org/scripts/script.php?script_id=1697)

下面用例子解释用法：

## 1. 修改（cs）

    "Hello world!" --> cs"' --> 'hello world!' --> cs'<q> --> <q>hello world!</q> --> cst" --> "hello world!"

## 2. 删除（ds）

    "hello world!" --> ds" --> hello world!

## 3. 给单个单词添加（ysiw）

`iw`是个text object，表示在单个单词添加

    hello world! --指针在hello上-- ysiw] --> [hello] world!

## 4. 给整句添加（yss）

    hello world! --> yssb or yss) --> (hello world) --> yss( --> ( (hello world) )

注意：使用左边括号会添加空格。

## 5. Visual mode（VS）：

{% highlight html %}
    hello world!
{% endhighlight %}

使用 `VS<p class="important">`

{% highlight html %}
<p class="important">
    hello world!
</p>
{% endhighlight %}

