koa2的中间件

```
1、koa-router
    全面的路由功能

2、koa-bodyparser
    支持x-www-form-urlencoded,application/json等格式的请求体，但不支持form-data的请求体
    或直接使用koa-body

3、koa-views
    需要进行视图模板渲染的应用，支持ejs等模板引擎

4、koa-static
    静态文件服务

5、koa-session
    HTTP是无状态协议，为了保护用户状态，用Session会话
    既支持将会话信息存储在本地Cookie，也支持存储如Redis、MongoDB这样的外部设备

6、koa-jwt
    使用nJWT认证HTTP请求

7、koa-helmet
    helmet通过增加如Strict-Transport-Security，X-Frame-Options，X-Frame-Options等HTTP头提高Express
    应用程序的安全性

8、koa-compress
    当响应体比较大时，会启用类似Gzip的压缩技术减少传输内容

9、koa-logger
    输出请求的日志的功能，包括请求的url、状态码、响应时间、响应体大小等信息

10、koa-convenrt
    比较老的使用Generate函数的koa中间件(<koa2)，进行将他们转为基于Promise的中间件Koa2使用
    兼容koa1，使用convert

好处：
    Koa精妙之处在于其使用generator和promise；
    Koa的中间件是一系列generator函数的对象，执行类似于栈的结构，依次执行；

了解koa中间件
    koa是由express原班人马打造的新一代web后端框架，
    相比express koa2更轻，代码也更优雅，
    优雅、简洁、表达力强、自由度高
    采用async await方式执行异步操作

    先进后出

    默认返回类型：text/plain

    koa对网络请求采用了中间件的形式处理，中间件可以介入请求和响应的处理，是一个轻量级的模块，
    每个中间负责完成特定的功能。
    中间件通过next()联系，执行next()后将控制权交给下一个中间件，
    如果没有中间件没有执行next后将会沿路返回，将控制权交换给前一个中间件。
    next()后面的代码会在后面中间件执行结束后执行

    koa2的中间件是通过async await实现
    中间件包含两个参数ctx，next

    ctx：
        作为上下文使用
        ctx.request
        ctx.response

        koa约定了一个中间件的存储空间：ctx.state
            通过state可以存储一些的数据

    koa2的中间件实现
        use
            const app = new Koa()
            app.use(logger)  //用来加载中间件

            app.listen(3000)

            koa实例对象app包含了一个数组属性middleware，通过use方法，将中间件push到数组
        
        callback
            当执行app.listen方法开启服务器时，实际是在内部使用http模块，启动了http服务器，
            并将自身的callback函数传入

        koa-compose
            可以将多个中间件合为一个

错误处理
    ctx.throw(500)：
                        抛出500错误
    ctx.response.status：
                        设置成404=ctx.throw(404)
    处理错误的中间件：
                        try...catch
    error事件的监听：
                        koa出错会捕获error事件
                        app.on('error',(error,ctx)=>{
                            
                        })
    释放error事件：
                        错误被try...catch捕获，就不会触发error事件，必须手动触发，才能让监听函数生效
                        调用ctx.app.emit()

Cookies
    ctx.cookies
        用来读写cookie
    koa-body
        可以用来从POST请求的数据体里面提取键值对；
        处理文件上传；
        

```