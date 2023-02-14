---
title: vue3从入门到放弃L01
date: 2022-07-26 22:44:30
tags: Vue
---

### 该来的躲不掉，vue3他终于向我伸出了双手，现在开始一起拥抱他吧。😩

### 对比Vue2与Vue3的一些区别

- Vue2只支持单节点，Vue3 template支持多节点，类似react fragments，新文件再也不需要外层包裹div节点啦！。
- 由Option aip 改为 Composition api，不会出现满屏的this了，数据的修改都在script中。
- style支持v-bind。
- TypeScript的支持，vue3由TS完全重写，完美支持TS。
- Proxy代替defineProperty，defineProperty无法实现对数组对象的深层监听，Proxy是浏览器最新api，功能更加强大。
- 全新的生态系统，vite代替webpack，Pina替代vuex，官方提供了更多的周边工具。
- 使用Hooks解决过去mixins的一些缺点。
- 当然最大的改变是不在支持IE，再也不用解决IE问题了，狂喜😍。

<br>

**接下来是重中之重点内容**

## 🍑 一、setup函数
