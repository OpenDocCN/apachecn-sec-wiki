<!--yml
category: 社会工程
date: 2022-11-10 10:29:58
-->

# 由王者荣耀查QQ引发的思考：抓包？头像接口找qq？uid找qq？-FancyPig's blog

> 来源：[https://www.iculture.cc/sg/pig=1267](https://www.iculture.cc/sg/pig=1267)

## 杂谈

最近有人询问能不能通过王者荣耀游戏查找QQ号，我用charles尝试进行了抓包，然后发现了几个有意思的事情，在本文中会跟大家分享

## QQ头像公开接口

首先给大家补充个小知识，如果做过开发的，下面的这个接口估计大家都不陌生，你只要通过输入你的QQ号就可以获取到头像的图片，并且是http的明文传输

*   QQ号按需填写
*   图片大小参数常见的是100、160、640（640的清晰度最高）

```
http://q.qlogo.cn/headimg_dl?dst_uin=你的QQ号&spec=图片大小参数
```

比方说我的QQ高清头像调用方式就是下方代码

```
http://q.qlogo.cn/headimg_dl?dst_uin=663962&spec=640
```

这也是为什么我之前会出一期专门的教程告诉大家可以通过万能的举报方式拿到uid，然后加到QQ

除了QQ的`小世界`，在此之前的QQ空间的匿名表白、坦白说、已经下线的QQ兴趣部落这些都存在可以通过举报uid、复制个人主页链接的方式查询到QQ，很多人在知道这个方法后都悄悄地找到了真爱，想想有点技术还是不错的哦。

## 王者荣耀抓包尝试

### 王者荣耀

我使用之前介绍的`Charles`试图对王者荣耀手游进行抓包

当然，你也可以使用`Fiddler`在电脑上对手机进行抓包，也可以使用`httpcanary`（我们常说的黄鸟）直接在安卓手机上抓包。总之，抓包工具有很多，选择一个适合自己的就行了。

然后，尴尬的事情就是我发现，王者荣耀手游已经使用的SSL协议进行了加密，导致在监控不到手机证书的情况下抓不到包

<figure class="wp-block-image size-large">![图片[1]-由王者荣耀查QQ引发的思考：抓包？头像接口找qq？uid找qq？-FancyPig's blog](img/a950eade7fe19797888406650dd1218a.png)</figure>

但是我还是找到了一种在王者荣耀里可以获取QQ的方法，分享给大家

### QQ游戏中心

在QQ游戏中心，我们可以看到游戏里的私信，也就是说你在游戏里只要给他发了消息，理论上就可以在QQ游戏中心添加好友

### 王者荣耀营地

如何通过王者荣耀营地找到游戏上的人呢？这里分为产生交互和不产生交互两种情况进行考虑

使用charles抓包，我随便打开了几个营地里好友的资料卡，可以看到头像居然是明文的

<figure class="wp-block-image size-large">![图片[2]-由王者荣耀查QQ引发的思考：抓包？头像接口找qq？uid找qq？-FancyPig's blog](img/a689871a8cd51c556395e0666886fa85.png)</figure>

但是并不是我们上面看到的公开接口，我随便取2个有特征的链接粘在下面

```
http://p.qlogo.cn/yoyo_avatar/488612565/0422de7055489a7a488ff07d32fe9657j/76
http://thirdqq.qlogo.cn/qqapp/1105200115/5EDA70419DC6194B5186C23DDDD8572C/100
```

先来分析一下，比较容易对比得到的线索吧。

第一个链接的其中一项内容比较容易解释，`488612565`这个是我的营地号，`76`应该是类似于我们上面讲公开接口的时候说的图片清晰度，这个`0422de7055489a7a488ff07d32fe9657j`估计是通过某种加密方式生成的头像hash值。

第二个链接中`1105200115`含义尚未明确，`100`应该是清晰度，`5EDA70419DC6194B5186C23DDDD8572C`估计也是通过某种加密方式生成的头像hash值。

## QQ头像加密算法的研究

通过研究，我们会发现QQ头像hash的加密方式

是通过`MD5(MD5(MD5(QQ号)+QQ号)+QQ号)`生成的32位的MD5码

我想，你现在是不是特别想骂人，”操你妈的这么写MD5不当人了吗“

当然，知道了原理我们是可以解决的，大不了就跑个程序的事情，给大家提供了一个简单的html的代码

后面，我也考虑了两种方式帮助大家解决上面的问题，仅针对`披萨会员`