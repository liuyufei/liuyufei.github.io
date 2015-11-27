---
layout:     post
title:      "Hello Jekyll"
subtitle:   " \"Hello World, Hello Jekyll Blog\""
date:       2015-11-27 12:47:00
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
* 自己造轮子 ... (程序员的病) 
* ...

作为程序员，个人博客这个东西肯定是要自己完全把控的，简单来说就是想要炫酷和装逼，自己不是专业前端大神，要想搞出高逼格的个人网站，就只能去网上找现成的东西来搭。

搜了一番觉得最好的还是 GitHub 这程序员的天堂，GitHub 提供了 GitHub Pages 来作为项目或者个人主页，结合 Jekyll 的轻量级博客框架就能任意构建自己的博客，Jekyll 使用 MarkDown 这种优雅的语言来写博客，且 GitHub 还免费提供了 Host 主机，真是省了一大笔心，服务器也不用搭了，还有免费的空间，博客更新更是使用 Git 的管理方式，只需管理对应的仓库就可管理自己的博客，真的是太符合程序员的口味了。

但是一路上搭建这个东西也是遇到了很多坑，这里就记录下整个 [GitHub Pages](https://pages.github.com/) + [Jekyll](http://jekyllrb.com/) + MacOSX 的搭建过程。

---

## 再讲东西

搭建这个东西需要涉及到的东西有 Ruby，Jekyll

#### 先装Ruby  

正好之前就有关注过 [GitHub Pages](https://pages.github.com/) + [Jekyll](http://jekyllrb.com/) 快速 Building Blog 的技术方案，非常轻松时尚。

其优点非常明显：

* **Markdown** 带来的优雅写作体验
* 非常熟悉的 Git workflow ，**Git Commit 即 Blog Post**
* 利用 GitHub Pages 的域名和免费无限空间，不用自己折腾主机
	* 如果需要自定义域名，也只需要简单改改 DNS 加个 CNAME 就好了 
* Jekyll 的自定制非常容易，基本就是个模版引擎


本来觉得最大的缺点可能是 GitHub 在国内访问起来太慢，所以第二天一起床就到 GitCafe(Chinese GitHub Copy) 迁移了一个[镜像](http://huxpro.gitcafe.io)出来，结果还是巨慢。

哥哥可是个前端好嘛！ 果断开 Chrome DevTool 查了下网络请求，原来是 **pending 在了 Google Fonts** 上，页面渲染一直被阻塞到请求超时为止，难怪这么慢。  
忍痛割爱，只好把 Web Fonts 去了（反正超时看到的也只能是 fallback ），果然一下就正常了，而且 GitHub 和 GitCafe 对比并没有感受到明显的速度差异，虽然 github 的 ping 值明显要高一些，达到了 300ms，于是用 DNSPOD 优化了一下速度。



---

配置的过程中也没遇到什么坑，基本就是 Git 的流程，相当顺手

大的 Jekyll 主题上直接 fork 了 Clean Blog（这个主题也相当有名，就不多赘述了。唯一的缺点大概就是没有标签支持，于是我给它补上了。）

本地调试环境需要 `gem install jekyll`，结果 rubygem 的源居然被墙了……后来手动改成了我大淘宝的镜像源才成功

Theme 的 CSS 是基于 Bootstrap 定制的，看得不爽的地方直接在 Less 里改就好了（平时更习惯 SCSS 些），**不过其实我一直觉得 Bootstrap 在移动端的体验做得相当一般，比我在淘宝参与的团队 CSS 框架差多了……**所以为了体验，也补了不少 CSS 进去

最后就进入了耗时反而最长的**做图、写字**阶段，也算是进入了**写博客**的正轨，因为是类似 Hack Day 的方式去搭这个站的，所以折腾折腾着大半夜就过去了。

第二天考虑中文字体的渲染，fork 了 [Type is Beautiful](http://www.typeisbeautiful.com/) 的 `font` CSS，调整了字号，适配了 Win 的渣渲染，中英文混排效果好多了。


## 后记

回顾这个博客的诞生，纯粹是出于个人兴趣。在知乎相关问题上回答并获得一定的 star 后，我决定把这个博客主题当作一个小小的开源项目来维护。

在经历 v1.0 - v1.5 的蜕变后，这个博客主题愈发完整，不但增加了诸多 UI 层的优化（opinionated）；在代码层面，更加丰富的配置项也使得这个主题拥有了更好的灵活性与可拓展性。而作为一个开源项目，我也积极的为其完善文档与解决 issue。

如果你恰好逛到了这里，希望你也能喜欢这个博客主题。

—— Hux 后记于 2015.10


