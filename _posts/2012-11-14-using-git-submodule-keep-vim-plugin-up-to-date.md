---
layout: post
title: 用 git submodule 同步 vim-plugins
categories: [Vim, Git]
tags: [Vim-plugin, Vim, Git, Github]
---

发表：[译言](http://article.yeeyan.org/view/5912/331981)

首先，你的 `vim` 配置文件得先有一个 `git repository`。

当我们为`vim`安装插件时，我们需要复制不同的文件到不同的目录，这让更新插件操作非常困难。
但现在很多`vim`的插件都有一个`github repository`。我们可以使用`git submodule`和`pathogen`插件来让这个操作变得容易点。

## 为 Vim 添加 bundle 支持

[Tim Pope](http://www.vim.org/account/profile.php?user_id=9012) 写了一个 vim 插件名叫 [pathogen](http://www.vim.org/scripts/script.php?script_id=2332) 。
这个插件可以让事情变得容易点。

这个插件，让你在你的`.vim/bundle`目录下管理你的插件，你可以在这个目录下对插件进行`unzip/untar/svn-checkout/git-clone` 操作。
这样，每一个插件不必被分裂复制到不同的目录，它们会待在同一个目录里，方便管理。

## 添加一个 Submodule

如果在`add submodule`之前，你已经用了一个插件（比如：`vim-fugitive`），那么你得先把它删掉：

{% highlight bash %}
git rm -r bundle/vim-fugitive
{% endhighlight %}

否则，你就会得的 `'vim-fugitive' already exists in the index` 的错误。

然后，我们添加 `vim-fugitive` 作为 `submodule`：

{% highlight bash %}
git submodule add git://github.com/tpope/vim-fugitive.git bundle/vim-fugitive
{% endhighlight %}

添加 `submodule` 之后，你还得 `register` 一下：

{% highlight bash %}
git submodule init
{% endhighlight %}

然后 `push` 就完成了。需要注意的是，以上所有命令操作都是在 `.vim`目录下进行的。

## 更新 submodule

更新submodule，使用：

{% highlight bash %}
git submodule update
{% endhighlight %}

## 更新 submodule 下的所有扩展

{% highlight bash %}
cd ~/.vim
git submodule foreach git pull origin master
{% endhighlight %}

## 删除 submodule

删除submodule，没有太有效率的方法，只能手动进行：

1. 手动删除 `.gitmodules` 和 `.git/config` 中的相关引用；
2. `git rm --cached bundle/vim-fugitive`

## 更多参考

- [Tips – Using git submodule keep your vim plugin up-to-date](http://www.allenwei.cn/tips-using-git-submodule-keep-your-plugin-up-to-date/)
- [github guides about submodule](http://github.com/guides/using-git-submodules-to-track-plugins)
- [github:Tim Pope](https://github.com/tpope)
- [github:vim-pathogen](https://github.com/tpope/vim-pathogen)
