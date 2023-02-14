---
title: eventBus
date: 2020-05-25 22:19:30
tags: JavaScript
---
哇，一转眼好几个月过去了，我的blog至今没有更新...

由于我实在太懒了，拖延症晚期，今天立了flag，一定要写两篇，刚好今天又接触到一个新的知识点。

## eventBus，一个vue 2.0时代前被我忽略的神奇操作

对于现在流行的前端开发模式（MVVM），经常涉及到多个组件间的通信，vue有vuex的支持，兄弟间组件传值很是方便，
自己写小程序的时候，苦于没有vuex类库，又觉得自己封装vuex有一点麻烦，兄弟间通信基本靠本地存储这种又笨又蠢的方法...
直到今天无意间发现了这个很好用的设计模式 --- eventBus， 之前面试的时候面试官也有问我了解么，我当时并没有听过，
和小伙伴 `@yogwang`聊天，他说这是vue1.0时代的产物，我也就没有特别关注过。
今天熟悉公司代码，无意间发现，诶，怎么这么多的bus.on方法的绑定呢，和小伙伴聊了聊发现，这是我错过的神奇方法。

### eventBus 举🌰说明

比如我们现在有三个组件，分别是父组件 - father, 哥哥组件 - brother, 妹妹组件 - sister，现在，哥哥想发微信给妹妹，要怎么样操作呢？
首先，我们给哥哥的手机下载一个微信，

```
<view bindtap="click">点击发送</view>
```
现在，想要把信息发送出去，我们需要建立一个基站，也就是bus.js。
然后，我们可以在基站内建立功能：
```
my.BUS = (function(){
  return {
    // 通过on来注册事件
    on: (name, callback) => {
        if (isString(name) && isFunction(callback)) {
            //防止多次注册触发
            my.BUS.off(name, callback);
            if (!events[name]) {
                events[name] = [];
            }
            events[name].push(callback);
        }
    },
    
    // 通过emit来触发事件
    emit: () => {

    },

    // 通过off来卸载事件
    off:() => {

    }
  }
}) ()
```
接下来，我们在哥哥的手机中编辑好要发送的消息
  ```
  click() {
    my.BUS.emit('msg', 'hello world')
  }
  ```
这样，妹妹就收到了哥哥发来的短信
```
my.BUS.on('msg', res => {
  console.log(res)
})
```
这个对于没有vuex类库的小程序来讲，作为兄弟组件间传值还是比较方便的。