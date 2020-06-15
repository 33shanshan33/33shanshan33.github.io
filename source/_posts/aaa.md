---
title: koa学习
date: 2020-06-09 12:05:28
tags:
---


### koa概念

基于Node.js平台的下一代web开发框架

<p><img src="/assets/koa_1.png" width="500"></p>
<!-- more -->

### 安装

~~~js
$ mkdir project

$ cd project

$ npm i --save koa

$ touch index.js  //编写koa内容

//index.js 内容
const Koa = require("koa");
const app = new Koa();

app.use(async (ctx) => {
  ctx.body = "Hello koa";
});

app.listen(3000);


~~~



### 启动

~~~js
$ node index.js //打开浏览器
~~~



### 工作原理

<p><img src="/assets/koa2.png" width="500"></p>

app.use()注册中间件 

每一个async函数称为一个middleware

await next()调用下一个async函数（也就是middleware）

```js
const Koa = require("koa");//引入koa
const app = new Koa(); //koa实例
const middleware = function async(ctx, next) {
  console.log("this is a middleware ");
  console.log(ctx.request.path);
  next();
};
app.use(middleware); //注册中间件

```

如果没有await next()，后续的middleware将不会执行，例如检测用户token时，没有就直接返回错误

