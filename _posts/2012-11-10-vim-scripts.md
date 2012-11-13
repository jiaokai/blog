---
layout: post
title: 我使用的Vim Plugins
categories: [Vim]
tags: [Vim, Vim-plugins, Code]
---

Vim 可利用其强大的插件功能实现几乎所有现在编辑器可能想象到的功能，下面几个是我经常使用的，
另外我感觉插件固然强大，但不要太贪杯，太多的插件容易引混乱。

## vim-pathogen

链接：[github](https://github.com/tpope/vim-pathogen) | [vim.org](http://www.vim.org/scripts/script.php?script_id=2332)

Vim 没有内建的插件管理器，安装插件只是把插件文件拷贝到你的`.vim`文件夹中即可，安装的方便却造成了管理的混乱。
要知道，每个插件都是由不同的作者开发，有些插件也会经常升级、修复bug。对插件进行版本管理，简直就是一场噩梦！

vim-pathogen 的是一个用来利用`git`来管理vim插件的工具。在你的`.vim`文件夹下新建`bundle`文件夹，然后`git clone`
你想要安装的插件即可。可以利用`git pull`方便的升级。

> Manage your `runtimepath` with ease. In practical terms, `pathogen.vim` makes it super easy to install plugins and runtime files in their own private directories.

将 `pathogen.vim` 放在 `~/.vim/autoload/pathogen.vim` 中，将新扩展利用 `git` 安装到 `~/.vim/bundle` 中。

{% highlight bash %}
    cd ~/.vim/bundle
    git clone git://github.com/tpope/vim-fugitive.git
{% endhighlight %}

## vim-surround

用于快速编辑可配对的标签，括号等，下面用实例来解释使用方法，`*`号代表光标所在位置：

{% highlight vim %}
    Old text                  Command     New text ~
    ----------------------------------------------------------------
    "Hello *world!"           cs"'        'Hello world!'
    "Hello *world!"           cs"<q>      <q>Hello world!</q>
    (123+4*56)/2              cs)]        [123+456]/2
    (123+4*56)/2              cs)[        [ 123+456 ]/2
    <div>Yo!*</div>           cst<p>      <p>Yo!</p>
    [123+4*56]/2              cs])        (123+456)/2
    "Look ma, I'm *HTML!"     cs"<q>      <q>Look ma, I'm HTML!</q>

    "Hello *world!"           ds"         Hello world!
    "Hello *world!"           ds"         Hello world!
    (123+4*56)/2              ds)         123+456/2
    <div>Yo!*</div>           dst         Yo!

    Hello w*orld!             ysiw)       Hello (world)!
        Hello w*orld!         yssB            {Hello world!}
    if *x>3 {                 ysW(        if ( x>3 ) {
    print "Hello *world!"     yss-        <?php print "Hello world!" ?>
    my $str = *whee!;         vllllS'     my $str = 'whee!';
{% endhighlight %}

详细介绍：`:h surround`。

## FuzzyFinder

这是我使用最频繁的一个plugin，它可让你在Vim中方面的查找各种文件，在我看来，对于文件的基本操作，使用这一个插件足矣。

## vim-fugitive

[github](https://github.com/tpope/vim-fugitive)

## zencoding

[github](https://github.com/mattn/zencoding-vim)

## vim-signature

[github](https://github.com/kshenoy/vim-signature)

## VimRoom

[VimRoom](http://projects.mikewest.org/vimroom/)

