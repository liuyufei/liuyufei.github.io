---
layout:     post
title:      "Hello Jekyll"
subtitle:   " \"Hello World, Hello Jekyll Blog\""
date:       2015-11-27
author:     "Jason.lyf"
header-img: "img/post-bg/post-bg-yaki.jpg"
tags:
    - Jekyll
---

> “终于终于，把这个搞起来了，经历了各种乱七八糟的问题”


## 先说废话

个人博客就这么弄起来了，直接放在了 GitHub Pages 上，没有自定义域名，还偶尔访问不上 GitHub ，且走且看吧。

很早之前就开始留意搭建博客的事情了，最直接想到的就是放到现有的论坛上，但是一是感觉CSDN，ITEYE这些地方的网站太丑，实在不想往上面放，二是如果想对自己的页面进行定制化这些地方就比较局限。

这里提供一些搭建博客的方式，感觉也都是不错的方式：

* [WordPress](https://wordpress.org/) (这个不用多说)
* [简书](http://www.jianshu.com/) (个人感觉也是个不错的选择，界面风格很赞)
* [Ghost](http://www.ghostchina.com/) (这个东西看着也是不错)
* 自己造轮子 ... (程序员的病) 
* ...

作为程序员，个人博客这个东西肯定是要自己完全把控的，简单来说就是想要炫酷和装逼，自己不是专业前端大神，要想搞出高逼格的个人网站，就只能去网上找现成的东西来搭。

搜了一番觉得最好的还是 GitHub 这程序员的天堂，GitHub 提供了 GitHub Pages 来作为项目或者个人主页，结合 Jekyll 的轻量级博客框架就能任意构建自己的博客，Jekyll 使用 MarkDown 这种优雅的语言来写博客，且 GitHub 还免费提供了 Host 主机，真是省了一大笔心，服务器也不用搭了，还有免费的空间，博客更新更是使用 Git 的管理方式，只需管理对应的仓库就可管理自己的博客，真的是太符合程序员的口味了。

但是一路上搭建这个东西也是遇到了很多坑，这里就记录下整个 [GitHub Pages](https://pages.github.com/) + [Jekyll](http://jekyllrb.com/) + MacOSX 的搭建过程。

---

## 再讲东西

搭建这个东西需要涉及到的东西有 **Ruby**，**Jekyll** 以及常用的 **Git**，我使用的是 Mac，系统版本是 **OS X EI Capitan 10.11**，系统默认自带2.0.0的 ruby 但是请**放弃使用**，建议使用 rvm 来管理 ruby 版本以及下载最新版的 ruby，保证安装过程正常。

在本地安装 Jekyll 只需要执行

```
gem install jekyll
```

但是如果你看到以下报错，就接着往下看吧

```
Building native extensions.  This could take a while...
ERROR:  Error installing jekyll:
	ERROR: Failed to build gem native extension.

    /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/bin/ruby extconf.rb
creating Makefile

make "DESTDIR="
make: *** No rule to make target `/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/include/ruby-2.0.0/universal-darwin15/ruby/config.h', needed by `yajl.o'.  Stop.


Gem files will remain installed in /Library/Ruby/Gems/2.0.0/gems/yajl-ruby-1.2.1 for inspection.
Results logged to /Library/Ruby/Gems/2.0.0/gems/yajl-ruby-1.2.1/ext/yajl/gem_make.out
```

#### 先装Ruby  

在装 ruby 之前，先安装 rvm 管理器：

```
curl -L get.rvm.io | bash -s stable
source ~/.bashrc
source ~/.bash_profile
```
为了加快 Ruby 安装速度，可以修改 Ruby 的安装源为[淘宝镜像服务器](https://ruby.taobao.org/)

```
sed -i -e 's/ftp\.ruby-lang\.org\/pub\/ruby/ruby\.taobao\.org\/mirrors\/ruby/g' ~/.rvm/config/db
```

装好 rvm 之后可以使用命令查看可以安装的 Ruby 版本，然后选择相应的版本进行安装

```
rvm list known

# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p643]
[ruby-]2.1.4
[ruby-]2.1[.5]
[ruby-]2.2[.1]
[ruby-]2.2-head
ruby-head
```

到这里应该都没有什么问题，但是当执行安装命令时，就会出现乱七八糟的问题

```
$ rvm install ruby-2.1.2

Searching for binary rubies, this might take some time.
Found remote file https://rvm_io.global.ssl.fastly.net/binaries/osx/10.11/x86_64/ruby-2.1.2.tar.bz2
Checking requirements for osx.
Installing requirements for osx.
Updating system - please wait
Installing required packages: libyaml, libksba - please wait
==> Upgrading 4 outdated packages, with result:
automake 1.15, libtool 2.4.6, openssl 1.0.2d_1, pkg-config 0.29
==> Upgrading automake
==> Downloading https://homebrew.bintray.com/bottles/automake-1.15.el_capitan.bottle.2.tar.gz

curl: (35) Server aborted the SSL handshake
Error: Failed to download resource "automake"
Download failed: https://homebrew.bintray.com/bottles/automake-1.15.el_capitan.bottle.2.tar.gz
Warning: Bottle installation failed: building from source.
==> Installing dependencies for automake: xz
==> Installing automake dependency: xz
==> Downloading https://homebrew.bintray.com/bottles/xz-5.2.2.el_capitan.bottle.tar.gz

....
```

错误太长，没有贴完，是在更新依赖工具 **automake**，**libtool**，**openssl** 和 **pkg-config** 的时候出错了，不是 SSL 连接断开就是源码编译出问题，这个时候就想翻个墙来解决这个问题，但又得一大堆配置，想想还是算了，找找别的方法吧，找了半天，后来在 [Ruby China](https://ruby-china.org/topics/22932) 论坛上面发现了解决办法，通过安装 xcode 的命令行工具包来安装这些依赖包

```
安装xcode 命令行工具：command line tools
方法： 在终端执行命令 xcode-select --install
```

安装完后，再次执行 `rvm install ruby-2.2.1` 即可顺利完成 Ruby 的安装

安装成功之后使用命令修改系统默认的 Ruby 版本

```
rvm use 2.2.1 --default 
```

#### 再装 Jekyll

为了方便在本地进行调试，就需要安装 Jekyll，否者每次修改之后需要往 GitHub 推送之后才能看到修改效果，在没有解决在本机上安装 Jekyll 之前，我试过一段时间，**不能忍！**

装完 Ruby 之后再次执行 `gem install jekyll` 进行 Jekyll 的安装就能够顺利的完成，但是这种方式安装 Jekyll 在以后会碰到很多问题，需要安装很多插件，在 GitHub Pages 的 Help 页面也说明了这个问题

> Jekyll - The main event. You'll want to create a file in your site's repository called Gemfile and add the line gem 'github-pages'. After that, simply run the command, bundle install and you're good to go. If you decided to skip step #2, you can still install Jekyll with the command gem install github-pages, but you may run into trouble down the line. 

所以这里推荐按照 GitHub Pages 的 [Help](https://help.github.com/articles/using-jekyll-with-pages/) 页面 [https://help.github.com/articles/using-jekyll-with-pages/](https://help.github.com/articles/using-jekyll-with-pages/) 来进行操作。

这里只给出在安装和使用的过程中碰到的一些问题

> 1、操作中会创建 Gemfile 文件，在页面中给出的样例为  
> 
> >	source 'https://rubygems.org'  
	gem 'github-pages' 
> 
> 在执行 bundle install 的时候可能会碰到连接问题，需要修改source，修改为 https://ruby.taobao.org 的国内源
> 
> >	source 'https://ruby.taobao.org'  
	gem 'github-pages'
> 
> 2、在后续的Jekyll使用过程中不要删除创建的 Gemfile 文件和 Gemfile.lock文件，会导致安装的插件失效，如果不小心删除了，重新创建 Gemfile 文件即可

#### Jekyll 模板

> 不是专业前端，放弃自己做模板

于是找啊找，找到了 [Clean Blog](https://github.com/IronSummitMedia/startbootstrap-clean-blog-jekyll) 以及 [Hux Blog](https://github.com/Huxpro/huxpro.github.io)，Hux 就是一个专业前端大神了，于是直接使用了他基于 Clean Blog 修改的主题，修改了配置和配图就直推送到 GitHub 上的 io 仓库了，然后就变成现在这个样子了，多亏了 Hux 的修改，这才搞的有模有样，膜拜 [@Hux](http://huangxuan.me/) 大神，他的博客同样也是放在了 GitHub Pages 上。

同样找背景配图也是得亏了有一个拍照极其棒的小伙伴 [@yaki](http://weibo.com/p/1005052095446005) 我才可以找到这么好的素材，谢啦！

到这里一个博客基本上也就搭出来了，来张预览

![preview](/img/post-content/hello_jekyll/preview.jpg)

---


## 最后

最后在个人喜好上改了代码显示的背景颜色，改成了和 GitHub 上面一样的代码显示风格，同时给图片显示加了阴影，后面自己也是打算能够丰富一下这个主题的功能，当然最重要的还是能够多写写东西吧。


