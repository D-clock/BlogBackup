---
title: Android开发：最详细的 Toolbar 开发实践总结
date: 2016-02-20
categories: Android
tags: [Android,UI效果]
---

过年前发了一篇介绍 Translucent System Bar 特性的文章 [Translucent System Bar 的最佳实践](http://blog.coderclock.com/2016/02/04/Android开发：Translucent%20System%20Bar%20的最佳实践/)，收到很多开发者的关注和反馈。今天开始写第二篇，全面的介绍一下 **Toolbar** 的使用。说起 **Toolbar** ，可能有很多开发的童鞋还比较陌生，没关系，请接着往下看。

<!-- more -->

## 初识 Toolbar

**Toolbar** 是在 Android 5.0 开始推出的一个 Material Design 风格的导航控件 ，Google 非常推荐大家使用 **Toolbar** 来作为Android客户端的导航栏，以此来取代之前的 **Actionbar** 。与 **Actionbar** 相比，**Toolbar** 明显要灵活的多。它不像 **Actionbar** 一样，一定要固定在Activity的顶部，而是可以放到界面的任意位置。除此之外，在设计 **Toolbar** 的时候，Google也留给了开发者很多可定制修改的余地，这些可定制修改的属性在API文档中都有详细介绍，如：

- **设置导航栏图标；**
- **设置App的logo；**
- **支持设置标题和子标题；**
- **支持添加一个或多个的自定义控件；**
- **支持Action Menu；**

![](https://diycode.b0.upaiyun.com/photo/2017/35c6ce74ff1c48ebc2f0e838634176e4.png)

总之，与 **Actionbar** 相比，**Toolbar** 让我感受到Google满满的诚意。怎样？是否已经对 **Toolbar** 有大概的了解，跃跃欲试的感觉出来了有木有？接下来，我们就一步一步的来看如何使用 **Toolbar**（其实是我使用 **Toolbar** 踩坑填坑的血泪史，你们接下去看，我先擦个眼泪.... ）。

## 开始使用 Toolbar

前面提到 **Toolbar** 是在 Android 5.0 才开始加上的，Google 为了将这一设计向下兼容，自然也少不了要推出兼容版的 **Toolbar** 。为此，我们需要在工程中引入 **appcompat-v7** 的兼容包，使用 **android.support.v7.widget.Toolbar** 进行开发。下面看一下代码结构，同样把重点部分已经红圈圈出：

![](https://diycode.b0.upaiyun.com/photo/2017/0d4607b0ea751c60638a305db492520d.png)

- ToolbarActivity 包含了 **Toolbar** 的一些基本使用， ZhiHuActivity 是在熟悉了 **Toolbar** 后对知乎主页面的一个高仿实现。

- layout和menu文件夹分别是上面提到的两个Activity的布局文件 和 actionmenu 菜单文件。

- values、values-v19、values-v21 中包含了一些自定义的 theme，后面用到的时候会顺带讲解。

我们先来看一下 ToolbarActivity 的运行效果

![](https://diycode.b0.upaiyun.com/photo/2017/2dfb20f80f78324129b157ac8ee38df1.gif)

按照效果图，从左到右分别是我们前面提及到的 **导航栏图标**、**App的logo**、**标题和子标题**、**自定义控件**、以及 **ActionMenu** 。接着，我们来看下布局文件和代码实现。

首先，在布局文件 activity_tool_bar.xml 中添加进我们需要的 Toolbar 控件

```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/color_0176da">

        <!--自定义控件-->
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Clock" />
    </android.support.v7.widget.Toolbar>
</LinearLayout>

```
接着在 base_toolbar_menu.xml 中添加 action menu 菜单项

```xml

<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <item
        android:id="@id/action_search"
        android:icon="@mipmap/ic_search"
        android:title="@string/menu_search"
        app:showAsAction="ifRoom" />

    <item
        android:id="@id/action_notification"
        android:icon="@mipmap/ic_notifications"
        android:title="@string/menu_notifications"
        app:showAsAction="ifRoom" />

    <item
        android:id="@+id/action_item1"
        android:title="@string/item_01"
        app:showAsAction="never" />

    <item
        android:id="@+id/action_item2"
        android:title="@string/item_02"
        app:showAsAction="never" />
</menu>

```

最后到 ToolbarActivity 中调用代码拿到这 **Toolbar** 控件，并在代码中做各种setXXX操作。

```java

/**
 * Toolbar的基本使用
 */
public class ToolBarActivity extends BaseActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_tool_bar);

        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        
        toolbar.setNavigationIcon(R.mipmap.ic_drawer_home);//设置导航栏图标
        toolbar.setLogo(R.mipmap.ic_launcher);//设置app logo
        toolbar.setTitle("Title");//设置主标题
        toolbar.setSubtitle("Subtitle");//设置子标题

        toolbar.inflateMenu(R.menu.base_toolbar_menu);//设置右上角的填充菜单
        toolbar.setOnMenuItemClickListener(new Toolbar.OnMenuItemClickListener() {
            @Override
            public boolean onMenuItemClick(MenuItem item) {
                int menuItemId = item.getItemId();
                if (menuItemId == R.id.action_search) {
                    Toast.makeText(ToolBarActivity.this , R.string.menu_search , Toast.LENGTH_SHORT).show();

                } else if (menuItemId == R.id.action_notification) {
                    Toast.makeText(ToolBarActivity.this , R.string.menu_notifications , Toast.LENGTH_SHORT).show();

                } else if (menuItemId == R.id.action_item1) {
                    Toast.makeText(ToolBarActivity.this , R.string.item_01 , Toast.LENGTH_SHORT).show();

                } else if (menuItemId == R.id.action_item2) {
                    Toast.makeText(ToolBarActivity.this , R.string.item_02 , Toast.LENGTH_SHORT).show();

                }
                return true;
            }
        });

    }

}

```

代码到此已经完成了 **Toolbar** 的基本使用，注意，是基本使用而已！！！！！下面有几个代码里面需要注意的地方：

1. 我们在使用 **Toolbar** 时候需要先隐藏掉系统原先的导航栏，网上很多人都说给Activity设置一个NoActionBar的Theme。但个人觉得有点小题大做了，所以这里我直接在BaseActivity中调用 **supportRequestWindowFeature(Window.FEATURE_NO_TITLE)** 去掉了默认的导航栏（注意，我的BaseActivity是继承了AppCompatActivity的，如果是继承Activity就应该调用**requestWindowFeature(Window.FEATURE_NO_TITLE)**）；

2. 如果你想修改标题和子标题的字体大小、颜色等，可以调用**setTitleTextColor**、**setTitleTextAppearance**、**setSubtitleTextColor**、**setSubtitleTextAppearance** 这些API；

3. 自定义的View位于 **title**、**subtitle** 和 **actionmenu** 之间，这意味着，如果 **title** 和 **subtitle** 都在，且 **actionmenu选项** 太多的时候，留给自定义View的空间就越小；

4. **导航图标** 和 **app logo** 的区别在哪？如果你只设置 **导航图标**（ or **app logo**） 和 **title**、**subtitle**，会发现 **app logo** 和 **title**、**subtitle** 的间距比较小，看起来不如 **导航图标** 与 它们两搭配美观；

5. **Toolbar** 和其他控件一样，很多属性设置方法既支持代码设置，也支持在xml中设置（这里也是最最最最最坑爹的地方，如何坑爹法，请接着往下看）；

## Toolbar 踩坑填坑

- **坑一：xml布局文件中，Toolbar属性设置无效**

刚开始使用Toolbar的时候，我的布局文件中是这样写的

```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/color_0176da"
        android:logo="@mipmap/ic_launcher"
        android:navigationIcon="@mipmap/ic_drawer_home"
        android:subtitle="456"
        android:title="123">

        <!--自定义控件-->
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Clock" />
    </android.support.v7.widget.Toolbar>
</LinearLayout>

```

在真机跑起来之后，看到的结果是下面这样的。

![](https://diycode.b0.upaiyun.com/photo/2017/147ccf37263d8cd111c9e959141570fb.png)

此时心中真是万千匹草泥马在奔腾，除了设置背景色和TextView有效外，说好的 **logo**、**navigationIcon**、**subtitle**、**title** 都跑哪去了？在编译器没报错又不见效果的情况下，参考了其他开发者的用法后找到了以下的解决方案，就是在根布局中加入自定义属性的命名空间

```xml

xmlns:toolbar="http://schemas.android.com/apk/res-auto"(这里的toolbar可以换成你想要其他命名，做过自定义控件的童鞋相比很熟悉此用法了)

```

然后把所有用 **android:xxx** 设置无效的，都用 **toolbar：xxx** 设置即可生效。最终的布局代码如下：

```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:toolbar="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/color_0176da"
        toolbar:navigationIcon="@mipmap/ic_drawer_home"
        toolbar:logo="@mipmap/ic_launcher"
        toolbar:subtitle="456"
        toolbar:title="123">

        <!--自定义控件-->
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Clock" />
    </android.support.v7.widget.Toolbar>
</LinearLayout>

```

到此即可解决 xml 中属性设置失效的问题，为什么会出现这种问题呢？我猜测是因为这个控件是兼容版的控件，用 **android:xxx** 设置无效是的这些属性是在兼容包中，不在默认的Android SDK中，所以我们需要额外的引入。至于为什么IDE不报错，估计就是bug了吧！

- **坑二：Action Menu Item 的文字颜色设置无效**

系统默设置了ActionMenu每个Item的文字颜色和大小，像ToolbarActivity在Google原生5.1系统下默认效果就是下面这样的

![](https://diycode.b0.upaiyun.com/photo/2017/fe2f90b5521d26473ba6c69472e45861.gif)

此时，如果我有需求要改变一下item文字颜色，应该怎么破？我按照网上比较普遍的解决方案，做了如下两步的修改操作：

- **在styles.xml中自定义一个Theme，并设置 actionMenuTextColor 属性（注意：不是 android:actionMenuTextColor ）**

```xml

<style name="Theme.ToolBar.Base" parent="Theme.AppCompat.Light.NoActionBar">
    <item name="actionMenuTextColor">@color/color_red</item>
</style>

```

- **在布局文件的Toolbar中设置popupTheme（注意：是toolbar:xxx，不是android:xxx）**

```xml

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/color_0176da"
        toolbar:popupTheme="@style/Theme.ToolBar.Base">

        <!--自定义控件-->
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Clock" />
    </android.support.v7.widget.Toolbar>

```

运行之后，文字的颜色的并没有发生任何改变。说好的改变颜色呢.....找来找去，最后在 StackOverflow 找到一个还不错的解决方案，就是把上面的的 **actionMenuTextColor** 属性换成 **android:textColorPrimary** 即可解决，最终得到下面的运行效果。

![](https://diycode.b0.upaiyun.com/photo/2017/fad3522b723f732dabe3337b77eff2f2.gif)

**这种方法也有一个小缺点，如果我把自定义控件换成Button，你会发现Button默认的文字颜色也变成了红色。所以，此处如果有朋友有更好的解决方案，请留言赐教。**

如果你想要修改 ActionMenu Item 的文字大小，也可以在theme中设置加上如下设置

```xml

<item name="android:textSize">20sp</item>

```

以上就是目前使用 **Toolbar** 一些比较折腾的坑，感觉 Google 对 **Toolbar** 这些坑，还可以进一步优化优化，不然就坑苦了开发者们了。

## 仿知乎主页面

为了加深一下 **Toolbar** 的开发体验，我们使用 **Toolbar** 来实现知乎主页的效果！先来看下知乎主页的效果

![](https://diycode.b0.upaiyun.com/photo/2017/78033598a1abd68c3ca8793685319458.gif)

如果前面的内容你看明白，想撸出这个界面无非是几分钟的事情，下面就直接上代码，不做赘述了。

ZhiHuActivity界面代码

```java

public class ZhiHuActivity extends BaseActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_zhi_hu);

        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        toolbar.inflateMenu(R.menu.zhihu_toolbar_menu);

        toolbar.setNavigationIcon(R.mipmap.ic_drawer_home);

        toolbar.setTitle(R.string.home_page);
        toolbar.setTitleTextColor(getResources().getColor(android.R.color.white));
    }
}

```

zhihu_toolbar_menu.xml 菜单

```xml

<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <item
        android:id="@id/action_search"
        android:icon="@mipmap/ic_search"
        android:title="@string/menu_search"
        app:showAsAction="ifRoom" />

    <item
        android:id="@id/action_notification"
        android:icon="@mipmap/ic_notifications"
        android:title="@string/menu_notifications"
        app:showAsAction="ifRoom" />

    <item
        android:id="@id/action_settings"
        android:orderInCategory="100"
        android:title="@string/menu_settings"
        app:showAsAction="never" />

    <item
        android:id="@id/action_about"
        android:orderInCategory="101"
        android:title="@string/menu_about_us"
        app:showAsAction="never" />
</menu>

```

activity_zhi_hu.xml 布局

```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@color/color_0176da"
        android:theme="@style/Theme.ToolBar.ZhiHu">

    </android.support.v7.widget.Toolbar>

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@android:color/white">

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:layout_centerInParent="true"
            android:background="@mipmap/ic_zhihu_logo" />
    </RelativeLayout>

</LinearLayout>

```

styles.xml 中的 Theme.ToolBar.ZhiHu，给 **Toolbar** 设置android:theme用的

```xml

<resources>

    ...
    ...

    <style name="Theme.ToolBar.ZhiHu" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="actionOverflowButtonStyle">@style/ActionButton.Overflow.ZhiHu</item>
    </style>

    <style name="ActionButton.Overflow.ZhiHu" parent="android:style/Widget.Holo.Light.ActionButton.Overflow">
        <item name="android:src">@mipmap/ic_menu_more_overflow</item>
    </style>

</resources>

```

最终得到下面这样的效果

![](https://diycode.b0.upaiyun.com/photo/2017/ffb28701b283dac9a6380e6b63919b30.gif)

这里在 **Toolbar** 设置 **android:theme="@style/Theme.ToolBar.ZhiHu"** 主要是为了替换系统右上角三个点的图标，如果不设置，则会成系统默认主题的样子。

![](https://diycode.b0.upaiyun.com/photo/2017/64ff0fc99cc6e5fdb876309783351542.png)

最后，再给知乎的主页面做个小小的优化，它在 Android 4.4 上运行还是能够看到一条黑乎乎的通知栏，为此我把 **Toolbar** 和 **Translucent System Bar** 的特性结合起来，最终改进成下面的效果（附上 Android4.4 和 5.1 上的运行效果）。

![](https://diycode.b0.upaiyun.com/photo/2017/40eed6bf1c817d35b5411d4ebf2aa326.png)

![](https://diycode.b0.upaiyun.com/photo/2017/5de2c6e2dc1657761f7ac7ac49633d7f.png)

如果你还不知道 **Translucent System Bar** 的特性怎么使用，请查看我的上一篇文章：[Translucent System Bar 的最佳实践](http://blog.coderclock.com/2016/02/04/Android开发：Translucent%20System%20Bar%20的最佳实践/)

## 总结

关于 **Toolbar** 的使用就介绍到此，本来是怀着很简单就可以上手的心态来使用，结果发现还是有很多坑需要填。果然还是验证了一句老话

```

纸上得来终觉浅，绝知此事要躬行

```

对于想要更深的了解 **Toolbar** 设计的童鞋，也可以看看这篇[官网文档](http://www.google.com/design/spec/components/toolbars.html)（自备梯子）。

同样，分享即美德，需要源代码的童鞋，请戳：https://github.com/D-clock/AndroidSystemUiTraining