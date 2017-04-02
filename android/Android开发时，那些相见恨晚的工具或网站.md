---
title: Android开发时，那些相见恨晚的工具或网站！
date: 2017-03-09
categories: Android
tags: [Android,开发工具,网站]
keywords: Android,开发工具,网站
---

**本文来我在知乎话题Android开发时你遇到过什么相见恨晚的工具或网站？下的回答！**

<!-- more -->

> [Android开发时你遇到过什么相见恨晚的工具或网站？](https://www.zhihu.com/question/27140400/answer/150729363)

在实际Android开发过程确实会有很多相见恨晚的工具或网站出现，下面是我自己的一些分享。

## 源码网站

> https://github.com/googlesamples

Android系统每次推出一些新特性，Google都会写一些Demo放在Github上，对于想要了解新特性怎么玩的同学，肯定不能错过它。

> https://www.codota.com/

如果你不知道一个Android的类怎么用，可以在Codota上面快速的找到很多不错的示例代码。

![](https://diycode.b0.upaiyun.com/photo/2017/8e41e146e9aa59e30783ba466e4a1fa4.png)

> https://android-arsenal.com/

你是否还在为找不到合适的开源库而苦恼，Android Arsenal这个网站已经帮你做了一定的分类，可以帮你提高不少效率。

>https://android.googlesource.com/

Android所有的源代码都在这里，只需找到对应想要的模块，用Git克隆下来即可。比如，我想要的framework代码

![](https://diycode.b0.upaiyun.com/photo/2017/77282bfa1d67607f2dea32cbb05cc0d1.png)

> http://androidxref.com/

克隆Android一个模块的代码量是很多的，有时候我只想要几个类的代码怎么办？AndroidXRef这个网站可以让你单独搜索某个类，要哪几个下载哪几个即可。

> http://grepcode.com/

除了AndroidXRef可以查看某个类的源代码外，GrepCode同样也能做到。而且GrepCode不限于Android的源码，这里也推荐一下。

## 源码分析

源码分析的网站很多，这里举几个比较经典的网站。

> http://a.codekk.com/

国内Android源码分析的先驱，由滴滴的技术专家Trinea发起，坦白的讲，这个项目对我的影响很大，我也从这里开始体会源码解读的魅力的。

> http://0xcc0xcd.com/p/index.php

老罗，罗升阳的个人博客站点，很多人看过他博客里面是如何分析Android和Chrome的源代码的。非常好的一个网站，以前功力不够没能看懂文章，经过一段时间后再回去翻看一些文章，不得不赞。

> http://gityuan.com/

GitYuan，MIUI系统工程师，他的博客经常分享Android系统源码解读的文章，质量很高。而且，更新频率也很高！

> https://github.com/LittleFriendsGroup/AndroidSdkSourceAnalysis

CJJ，猪场（网易）的开发者，由他带领发起的Android SDK源码解析，同样推荐。

##酷炫动画

> https://github.com/airbnb/lottie-android

Airbnb开源的动画库，为什么推荐它，是因为它让复杂酷炫的动画效果轻松实现了，不仅提高工程师的效率而且性能非常客观。我在YY工作，内部已经有一套和它实现原理一样的框架，所以看到Lottie的时候，一点不觉得奇怪，考虑可能还有不少童鞋应该还不知道它，这里再推荐一下。（PS：Lottie还有iOS、React Native、Web端的实现哦）

![](https://diycode.b0.upaiyun.com/photo/2017/efdc365134813f9f6cda1df827aaf726.gif)

## Crash搜集

> https://bugly.qq.com

Bugly，腾讯出品的SDK，对Crash搜集的体验非常赞，能搜集到JNI层的奔溃以及监控线上的ANR问题。

> https://try.crashlytics.com/

Crashlytics，国外的一个SDK，我自己没用过，但是用过的朋友对它的评价颇高。

> https://github.com/ACRA/acra

ARCA，一个开源的崩溃日志搜集器，轻松让你实现客户端的崩溃日志上传到后台，如果你不喜欢接入别人家的SDK，可以使用它。有一个不足之处，就是它搜集不到JNI层的奔溃。

##逆向分析

逆向分析工具太多，举几个经典的做例子。

> https://github.com/skylot/jadx/

Jdax，轻轻一下，立马让apk宽衣解带，下面是我拿知乎开刀的例子。

![](https://diycode.b0.upaiyun.com/photo/2017/8f986e328079cea9d6b69080a27ed604.png)

> https://github.com/google/android-classyshark

Classyshark，轻松查看apk内部每个包的方法数，用了哪些开源库，同样拿知乎开刀做例子。

![](https://diycode.b0.upaiyun.com/photo/2017/e73af1c00959f05faa326dbc4268a31a.png)

> https://github.com/JesusFreke/smali/wiki/smalidea

smali代码调试插件，你以为没有拿到安卓Java源码就不能调试了吗？图样图森破了吧。

![](https://diycode.b0.upaiyun.com/photo/2017/9883fefebb28734dff14248b35956a45.png)

> https://www.hex-rays.com/products/ida/

IDA Pro，逆向大利器，不管你是smali还是so文件，照样动态调试你。

**注意，这些用来涨知识就好，别干坏事！**

## AS插件

Android Studio插件很多，只推荐两个我常用的。

> https://github.com/mcharmas/android-parcelable-intellij-plugin

帮助继承Parcelable的类自动生成相应代码，在没遇见它之前，手动写过大量的Parcelable实现代码，真的好痛苦。

![](https://diycode.b0.upaiyun.com/photo/2017/1f00250b7eff8f4e54b74d7dc77e3f85.png)

> https://github.com/zzz40500/GsonFormat

根据JSON数据快速生成Java实体类，又一波解放生产力。

![](https://diycode.b0.upaiyun.com/photo/2017/d99a4b81e1400fddc947ebef8a7072ac.gif)

## 调试利器

> http://facebook.github.io/stetho/

Stetho，来自Facebook，它能做什么？无需root，借助Chrome可以查看SharePreferences和数据库中的数据，此外还有网络抓包以及查看View树等。

![](https://diycode.b0.upaiyun.com/photo/2017/c9f4cab15b67c0b6d17c6334c86c9ebf.png)

## 性能优化

> http://hukai.me/

胡凯，腾讯开发者，翻译了一系列的Google Android性能优化典范的文章。

> https://hujiaweibujidao.github.io/

Hujiawei，魅族开发者，博客最近经常更新Android性能数据搜集统计的相关的文章，本人受益匪浅。

## 最后 

零零散散大致就分享一下这些，喜欢我的文章可以并关注我的微信公众号：**技术视界**，以及关注我的[知乎](https://www.zhihu.com/people/d_clock)和[知乎专栏](https://zhuanlan.zhihu.com/coderclock)

![](https://diycode.b0.upaiyun.com/photo/2017/a3fc893f2cf4d4ab33ac32666d00a793.jpg)
