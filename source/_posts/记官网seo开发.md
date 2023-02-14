---
title: 记官网seo开发【nuxtJS】
date: 2022-05-03 13:00:35
tags: seo nuxt
---

近期公司要做一个知识库网站，由于一直在做spa项目，需要seo的网站已经很久没有做过了，借着这次机会补充一下。
由于我司都是JAVA，所以技术选型还是以前后端分离为主，之前有考虑模版引擎的写法做，但是项目很赶，需要其他同事支援，考虑开发时间，最后选择了 [nuxtJS](https://nuxtjs.org/ "nuxtJS")。

*****
Nuxt是基于vue开发的服务器端渲染框架，利用 SSR（也叫做 "universal" or "isomorphic" 模式），Node.js 服务器将基于 Vue 的组件渲染成 HTML 并传输到客户端，而不是纯 javascript。与传统的 Vue SPA 相比，使用 SSR 将带来巨大的 SEO 提升、更好的用户体验和更多的机会。

当然Nuxt也支持spa，但使用它不就是为了SSR么～

### 🍑 安装 ###
Nuxt.js 团队创建了脚手架，使用yarn命令安装即可
```
$ yarn create nuxt-app <项目名>
```
接下来会让你进行一些项目配置的选择，选择你喜欢的框架。
### 🍑 目录结构 ### 
关于目录结构，这个是重点，我会一一介绍并说明：

- assets 资源目录，用于存放未编译的静态资源，css，js，image等
- components 组建目录，用于存放组建，但千万注意，该目录下文件不支持`asyncData`方法特性（该方法为Nuxt特有生命周期，下面会说到）。
- layouts 布局目录，用作页面整体布局使用。
- middleware 中间件目录，允许用户自定义函数运行在一个页面或一组页面渲染前，通常会存放路由守卫，请求头等，执行顺序为，nuxt.config.js= -> layout下布局 -> 页面。

- pages 页面目录，Nuxt.js会读取该目录下`.vue`文件并自动生成对应路由配置

- plugins 插件目录，类似于vue中`main.js`，在vue.js实例化前需要运行的Js插件，比如swiper.js。
- static 静态资源文件，不会被webpack编译处理，会映射在应用根路径`/`下
- Store Vuex状态树，在`Store`目录创建一个index.js文件可激活配置
- nuxt.config.js文件 Nuxt.js应用个性化配置。
- package.json文件 用于描述应用的依赖关系和对外脚本接口。

### 🍑 别名
`～` 或 `@` srcDir

`～～` 或 `@@` rootDir

默认情况下，`srcDir` 和 `rootDir`相同
### 🍑 插件引入`plugins`

 `要注意对应插件引入的路径`，这很重要:
```
import Vue from 'vue'
import 'swiper/dist/css/swiper/css'
import VueAwesomeSwiper from 'vue-awesome-swiper/dist/ssr'

Vue.use(VueAwesomeSwiper)
```

然后，在nuxt.config.js内配置`plugins`:
```
module.exports = {
  plugins: [{src: '@/plugins/vue-awesome-swiper', mode: 'client'}] // client 为不开启服务端渲染(ssr)，默认开启
}
```
### 🍑 中间件`middleware`

你可以在nuxt.config.js、layouts或者pages中使用中间件：

`nuxt.config.js`

```
module.exports = {
  router: {
    middleware: 'xxx' // 如果是多个，使用数组
    base: process.env.NODE_ENV === 'production' ? './' : '' // 非顶级目录情况下
  }
}
```

`layouts && pages`

```
export default {
  middleware: 'xxxx'
}
```
### 🍑 打包运行

### 🍑 请求

### 🍑 适配
