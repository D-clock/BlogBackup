---
title: Android应用继续瘦身，以及一些注意事项
date: 2017-04-17
categories: Android
tags:  [Android,应用瘦身,性能优化]
---

自上次对应用瘦身过后，经历的若干功能的迭代，很快的，安装包大小又到了15MB，老大说要控制在10MB之内，于是便开始了新一轮的瘦身之旅。

<!-- more -->

如果你还没读过我的前面一篇瘦身文章，可以先去看看：

> [Android应用瘦身，从18MB到12.5MB](http://blog.coderclock.com/2017/01/24/android/Android%E5%BA%94%E7%94%A8%E7%98%A6%E8%BA%AB%EF%BC%8C%E4%BB%8E18MB%E5%88%B012.5MB/)。

已经看过上文的朋友，可以直接阅读本文，文章接下来将会为你带来更多瘦身方案，以及一些需要注意的问题。

## WebP处理

在我的上一篇文章提到，让大家谨慎使用WebP格式的图片，并且提及到Android Studio不支持预览WebP图片的问题，而最新的2.3版本已经支持预览WebP文件，同时还能够帮我们将JPG和PNG转换成为WebP图片，虽然IDE的升级让我们喜出望外，但你仍然要关心WebP的一下几个问题：

- WebP的编码时间为PNG的5倍以上，解码速度与PNG差不多，甚至更快；
- WebP编码时占用内存比PNG高25%，解码时比PNG低30%；
- Android 4.0+开始支持WebP图片，但是带透明度的WebP图片是在4.2.1+之后才支持的，在4.2.1之前则无法显示；

针对以上一二点，你可能需要考虑一下自家用户实际机型分布情况，如果大部分都是中低端配置机型，使用了WebP后对体验可能会有所下降，对于高配设备，完全可以忽略。而针对第三点，则需要考虑用户的系统分布，相信绝大部分App的用户已经满足4.0+这个条件，但对于满足4.2.1+条件就很难说了，至少我们这款有几百万用户的产品仍有不少用户不满足此条件，因此也不敢随便提升最低兼容版本，但是你仍然可以进行一些WebP的处理，主要如下：

- 对于不需要透明度的PNG图片，先转成JPG格式后，再使用IDE进行WebP转换。不要直接用PNG转换成WebP，否则转换后的WebP仍然带了透明度，在4.2.1之前的设备任然无法显示，先转换成JPG就是为了去除PNG的透明度；
- 将PNG转换成JPG时，建议采用专业的图片处理工具，因为我在使用一些在线转换工具转换成为JPG时，发现有少量的图片转换成JPG后再转成WebP时在4.2.1之前依然无法正常显示，但经过专业的处理的图片处理工具转换后的图片则全部没有问题；
- 在将JPG转换成WebP图片时，采用IDE默认75的有损压缩质量，超过75之后，压缩效果反而会变差；

虽然IDE给了我们WebP更方便的支持，但实际上受限于Android系统版本的问题，所以，我们只能对有限的图片做处理，对于项目中有大量留白的透明像素的图片，转换成JPG效果会失真，所以，也只能暂时忽略掉。最后，推荐一个腾讯出品的WebP在线工具——智图：https://zhitu.isux.us/ 。

关于WebP的知识，我非常建议大家阅读以下两篇腾讯出品的文章，你会收获很多

- [WebP原理和Android支持现状介绍](https://mp.weixin.qq.com/s/BPGqVZXUJs3RvJwrznRttQ)
- [WebP探寻之路](http://isux.tencent.com/introduction-of-webp.html)

## shrinkResources

http://www.cnblogs.com/tianzhijiexian/p/4457763.html

https://developer.android.com/studio/build/shrink-code.html#shrink-resources

https://juejin.im/entry/580cdf4267f3560057bbae98

## resConfigs

## SO压缩

## Dex文件

## 第三方依赖

## 项目源码精简

提及插件化，但是因为是另一范畴的话题，本文就不展开叙述。

## AndResGuard

## Redex

## 总结



**欢迎关注我的微信公众号：技术视界**

![](https://diycode.b0.upaiyun.com/photo/2017/a3fc893f2cf4d4ab33ac32666d00a793.jpg)
