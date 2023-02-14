---
title: js骚操作
date: 2020-05-26 11:36:50
tags: JavaScript
---

## 动态变量名

```
let aaa = 'bbb'
const obj = {
  [`a`]: 123
}
console.log(obj)
// { bbb: 123 }
```