---
title: 'h5页面打开app，安卓端和苹果端'
date: 2020-02-27 21:26:20
tags: H5
---
对于App的分享页面，移动端经常会遇到需要唤起App并定位的功能。

### 跳转到App方法

安卓通常使用 URL Scheme 方法
IOS有两种方法 meta标签和Universal Links， 我们通常使用Universal Links

## URL Scheme

URL Scheme就是一个可以让app相互之间可以跳转的对外接口。每个app都不同，如果有重复的会响应先安装的app。URL Scheme的格式为：
``` bash
[scheme]://[host]/[path]?[query]
```
比如：
+ 淘宝： taobao://
+ QQ： mqq://
+ 微信： weixin://

## meta标签
在网页上设置meta标签，使用safari打开的时候，就会在顶部显示自己app的导航条。如果没有安装app点击能够跳转到appstore去下载，如果安装了app就能直接通过顶部的meta标签唤醒app了。（此为IOS特有）
``` bash
 <meta charset="UTF-8" name="apple-itunes-app" content="app-id=yourId, affiliate-data=myAffiliateData, app-argument=yourScheme://">
```
## Universal Links
iOS 9之前，一直使用的是URL Schemes技术来从外部对App进行跳转，但是iOS系统中进行URL Schemes跳转的时候如果没有安装App，会提示Cannot open Page的提示，而且当注册有多个scheme相同的时候，目前没有办法区分，但是从iOS 9起可以使用Universal Links技术进行跳转页面，这是一种体验更加完美的解决方案

## 实现唤醒APP功能
大多数需要唤醒app时都是在微信内，但由于微信内部禁用了唤醒功能，所以做了一个引导页，引导用户通过浏览器打开。（一些知名app可以唤起）
```bash
<div class="main">
  <div class="tips" id="ios"></div>
  <div class="tips" id="android"></div>
  <div class="logo"></div>
  <div class="info"></div>
  <div id="a-btn" class="downloadBtna"><a href="https://wwww.******.com.cn/api/app/download"></a></div>
  <div id="i-btn" class="downloadBtni"><a href="https://itunes.apple.com/cn/app/yourId"></a></div>
</div>

// 获取浏览器用于 HTTP 请求的用户代理头的值
var u = navigator.userAgent, ua = u.toLowerCase()
var isWeiXin = ua.indexOf('micromessenger') != -1;
var {isAndroid, isIOS} = detectVersion()
// 获取参数id值、来源值，以便用于scheme跳转
var id = getQueryString('id')
var source = getQueryString('source')
// 判断当前浏览器
function detectVersion() {
  var isAndroid, isIOS;
  if(u.indexOf('Android') > -1 || u.indexOf('Linux') > -1) {      // android or uc browser
      // android
      isAndroid = true
  }
  if(ua.indexOf("like mac os x") > 0) {
      isIOS = true
  }
  return {isAndroid, isIOS}
}
// 唤起app方法
function openApp(callback) {
  var url = ""
  if (isAndroid ) {
    url = '[scheme]://'+ source +'?id=' + id
    var timeout, t = 3000, hasApp = true
    var openScript = setTimeout( function () {
      if (!hasApp) {
        callback && callback()
      }
      document.body.removeChild(ifr)
    },5000)

    var t1 = Date.now()
    var ifr = document.createElement("iframe")
    ifr.setAttribute("src", url)
    ifr.setAttribute("style", "display:none")
    document.body.appendChild(ifr)
    timeout = setTimeout( function () {
      var t2 = Date.now()
      if (t2 - t1 < t + 100) {
        hasApp = false
        // 此处创建一个定时器，以便用于判断页面是否跳转，如果未成功跳转，那么判断未安装app，此时跳转到app下载
        window.location.href="https://www.******.com.cn/api/app/download"
      }
    },t)
  }
  if (isIOS) {
    // Universal Links 需要IOS工程师进行配置
    window.location.href= "https://www.******.com.cn/" + source + "?id=" + id
  }
}
$(function () {
  if(isWeiXin) {
    if(isAndroid) {
      $("#a-btn").show()
      $("#android").show()
    } else {
      $("#i-btn").show()
      $("#ios").show()
    }
  } else {
    if(isAndroid) {
      $("#android").show()
      $("#a-btn").show()
      openApp()
    } else {
      $("#ios").show()
      $("#i-btn").show()
      openApp()
    }
  }   
})
```

### 以上并为考虑ios9以下版本