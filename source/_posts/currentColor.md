---
title: currentColor
date: 2021-04-13 17:44:32
tags: css3
---
## css3中强大的属性currentColor
今天在日常开发中遇到了一个需求，需要切换伪类的背景色。
然后我尝试了各种办法，甚至用到了css的变量法都没能实现，然后我就找小伙伴去聊这个问题，看看他有没有什么好方法。
他给我提供了两个方案：
1.继承父级的背景色
2.用currentColor，继承父级的文字颜色currentColor

当我看到currentColor时，一脸的问号？？？ 这货是啥，vue貌似没有这个参数吧。

然后我简单谷歌了一下，what，这个东西好骚，我喜欢。
简单介绍一下 `currentColor`, 他是css3属性，可以继承最近的父级的`color`属性, 兼容性也不错，ie9+以上都可以，基本上市面上主流浏览器都可以了。

接下来介绍一下如何使用
```
.father {
  color: red;
}
.father::after {
  background: currentColor;
}
```
是不是很简单？ 对，就是这么简单，只要更改父级的color属性，那么伪类就可以继承父级的color颜色了。这样我们就可以动态的更改伪类的颜色了。
