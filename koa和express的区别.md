koa和express的区别

```
    koa比express更精简，它有足够的扩展和中间件，

    express：
        基于Node平台的极简、灵活的web应用开发框架，主要基于Connect
        中间件，并且自身封装了路由、视图处理等功能。
    Koa：
        更为年轻，主要基于co中间件，框架自身不包含任何中间件，很多功能需要
        借助第三方中间件解决，但是其基于ES6 generator特性的异步流程控制，
        解决了callback hell和麻烦的错误处理问题，大受开发者欢迎。

1、    express是自身集成的
        var express=require('express')
        var app=express()

        app.get('/',function(req,res){
            res.send('Hello World')
        })
        app.listen(3000)

    Koa需要引入中间件
        var koa=require('koa')
        var route=require('koa-router')
        var app=koa()

        app.use(route.get('/',function *(){
            this.body='Hello World'
        }))

        app.listen(3000)

2、Views
    Express自身集成了视图功能，支持几乎所有JavaScript模板引擎，并提供了视图设置的便利方法；

    Koa需要引入co-views中间件

3、HTTP Request
    两个框架都封装了Http Request对象，
    不同的是Koa v1使用this取代Express的req、res

4、异步流程控制
    Express采用callback来处理异步
    Koa v1采用generator
    Koa v2采用async await

    generator和async/await使用同步的写法来处理异步，明显好于callback和promise
    async/await语义化上比generator更强

5、错误处理
    Express使用callback捕获异常，对于深层次的异常捕获不了
    Koa使用try catch，能更好的解决异常捕获

总结：
    express：
        优点：
            线性逻辑，通过中间件形式把业务逻辑细化、简化，
            一个请求进来经过一系列中间件处理后再响应给用户，清晰明了。
        缺点：
            基于callback组合业务逻辑，业务逻辑复杂时嵌套多
            异常捕获困难
    koa：
        优点：
            借助co和generator，很好地解决了异步流程控制和异常捕获问题
            koa把express内置的router、view等功能移出了，使框架本身更轻；
        缺点：
            社区相对较小

```