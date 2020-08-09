## 2.1 Nodejs web框架及koa

### 2.1.1 Nodejs常见的框架

| 框架名称  |  特性  | 评价 | 
| :------: | :-----: | :---: |
| Express | 简单、实用、路由中间件等五脏俱全 |  最著名web框架  | 
|  Hapi&Restify | 面向API&微服务 |  移动互联网时代API作用被放大，故而独立分类，尤其是对于微服务开发更是利器  |
| ThinkJS   | 面向新特性 |  借鉴ThinkPHP，并慢慢走出自己的一条路，长于新特性执行，新版V3.0是基于Koa2.0的作为内核的  |
|  Koa  | 专注于异步流程改进 |  下一代web框架  |
|  Egg  | 基于Koa，在开发上有极大的便利|  企业级Web开发框架  |

### 2.1.2 Koa概览

- Express很简洁，Koa更简洁
- Koa应用程序是一个包含一组中间件函数的对象，它是按照类似堆栈的方式组织和执行的
- 内置优雅的底层中间件处理内容协商，缓存清理，代理支持和重定向等常见任务的方法，开箱即用

#### 洋葱模型

请求一层层的进入，一层层的退出，也就是说先进的后出，后进的先出

![](~@/node/onionmodel.png)

从下面代码可以看出，完全是遵循洋葱模型从1-9执行过程，通过next把模块串联起来，koa的洋葱模型允许我们加入很多中间件的处理

```js
const Koa=require('koa')
const app=new koa()

// x-response-time

app.use(async (ctx,next)=>{
    const start= Date.now() //1
    await next() // 2
    const ms=Date.now()-start // 8
    ctx.set('X-Response-Time',`${ms}ms`) // 9
})

// logger

app.use(async (ctx,next)=>{
    const start= Date.now() //3
    await next() //4
    const ms=Date.now()-start //6
    ctx.set(`${ctx.methods}${ctx.url}-${ms}`) //7
})

// reponse

app.use(async ctx=>{
    ctx.body='Hello World' //5
})

app.listen(3000)

```

#### Koa常见的中间件

- koa-static处理静态资源
- koa-router 处理路由
- koa-session 保存网络请求状态
- koa-bodyparser 处理请求体
- koa-compress 压缩响应数据
- koa-logger 输出服务日志
- koa-error 处理响应错误

### 2.1.3 使用Koa编写web Server

#### REST 接口设计-路由

```js
   //接口要遵循http动词
  GET /xhr/v1/templateList // 获取模版列表
  GET /xhr/v1/templateDetail?id=xx   // 模版单个模版详情
  POST /xhr/v1/templateCreate // 创建模版
  PUT  /xhr/v1/templateChange/1 // 修改模版,
  DELETE /xhr/v1/templateDelate/1 // 删除模版
```

我们使用社区提供的优秀脚手架去构建项目,github上搜索`awesome-koa`可以找到koa相关社区资源，例如：`https://github.com/fineen/awesome-koa`，在文档里找到这`koa-rest-api-boilerplate `这个脚手架;一个小技巧，以awesome为前缀去找框架相关资源。

```bash
  # --depth表示克隆深度，1表示克隆最进一次的commit
 git clone --depth=1 https://github.com/posquit0/koa-rest-api-boilerplate.git
 cd koa-rest-api-boilerplate
 rm -rf .git && git init
```
看一个框架，首先看`package.json`文件，看脚本运行了哪些命令，然后看入口文件。


### 2.1.4 扩展学习资料

[Koa官网](https://koajs.com/)
[Koa源码](https://github.com/koajs/koa)
[Awesome](https://github.com/fineen/awesome-koa)
[Koa2快速开发入门](https://juejin.im/post/5c6eb4ac6fb9a049d4426ab2)