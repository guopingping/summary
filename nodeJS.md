```
Node同其他框架语言的比较：
    Node特色的非阻塞IO和异步性
    单线程是非阻塞的IO模型，就是一个线程结束，紧接着另一个线程开始，就是单通道的。

常用js类定义的方法：
    构造函数方法定义类
    对象创建方法定义类

什么是闭包？有哪些用处？
    函数：更多字嵌套函数的父子自我引用关系，所有函数都是闭包。
    闭包就是作用域范围

defineProperty、hasOwnProperty、isEnumerable
    Object.defineProperty(obj,prop,descriptor):用来给对象定义属性
    hasOwnProerty：用于检查某一属性是不是存在于对象本身，继承来的父亲的属性不算
    isEnumerable：用来检测某一属性是否可遍历

node
    简单强大，可轻量扩展，体现在node使用的是JavaScript，json来进行编码；
    强大体现在非阻塞IO，可使用分块传输数据，较慢的网络环境，擅长高并发访问
    轻量体现在node本身既是代码，又是服务器，前后端使用统一语言；
    可扩展体现在可以轻松应对多实例，多服务架构，同时海量的第三方应用组件；

node核心模块
    EventEmitter，Stream，FS，Net和全局对象

node全局对象
    process，console，Buffer和exports

process常用的方法
    process.stdin，process.stdout, process.stderr, process.on ,process.env , process.argv,
    process.arch,process.platform,process.exit

console常用的方法
    console.log/console.info console.error/console.warning
    console.time/console.timeEnd  console.trace console.table

node定时功能
    setTimeout/clearTimeout  setInterval/clearInterval
    setImmediate/clearImmediate process.nextTick

node事件循环是什么样子的
    event loop：事件队列，先加入先执行，执行完一次队列，再次循环遍历看有没有新事件加入队列。
    执行中的叫IO events，setImmediate是在当前队列立即执行，
    setTimeout/setInterval是执行定时到下一个队列
    process.nextTick是在当前执行完，下次遍历前执行
    所以总体顺序是：
        IO events >> setImmediate >> setTimeout/setInterval >> process.nextTick

EventEmitter？
    node中一个实现观察者模式的类，监听和发射信息，用于处理多模块交互问题

什么是Stream？
    stream是基于事件EventEmitter的数据管理模式，由各种不同的抽象接口组成，包括可读、可写、可读写、可转换

    好处
       非阻塞式数据处理提升效率，片断处理节省内存，管理处理方便可扩展等；

    典型应用
        文件、网络、数据转换、音频视频

    捕获stream错误事件
        监听error事件

    常用的stream
        Readable可被读流，作为输入数据源时使用；
        Writable可被写流，在作为输出源时使用；
        Duplex可读写流，作为输出源接受被写入，作为输入源被后面的流读出；
        Transform机制和Duplex一样，双向流，区别：Transform只需实现一个函数_transform(chunk,encoding,callback)
        ,Duplex需要分别实现_read(size)和_write(chunk,encoding,callback)函数

文件系统
    内置的fs模块架构是什么样子的？
        POSIX文件Wrapper，对应于操作系统的原生文件操作；
        文件流fs.createReadStream和fs.createWriteStream
        同步文件读写 fs.readFileSync 和fs.writeFileSync
        异步文件读写 fs.readFile 和 fs.writeFile
    
    读写一个文件有多少中方法？
        POSIX式底层读写
        流式读写
        同步文件读写
        异步文件读写

    如何读取json配置文件
        第一：利用node内置的require('data.json')机制，直接得到js对象
        第二：读入文件入内容，然后用JSON.parse(content)转换为js对象
        两者区别：
            第一种：require机制，如果多个模块都加载了同一个json文件，则其中一个改变了js对象，其它跟着改变
            这是由node模块的缓存机制造成的；
            第二种则可以随意改变加载后的js变量，而且个模块互不影响，因为他们都是独立的，是多个js对象；
    
    fs.watch和fs.watchFile区别：
        监听文件变动
        fs.watch利用操作系统原生机制来监听，不适用网络文件系统；
        fs.watchFile定期检查文件状态变更，适用于网络文件系统，但是比fs.watch有些慢，因为不是实时机制
    
网络

child-process
    为什么需要child-process?
        把node阻塞的工作交给子进程去做；
    
    exec,execFile,spawn,fork
        exec：可以用操作系统原生的方式执行各种命令
        execFile：执行一个文件
        spawn：流式和操作系统进行交互
        fork：两个node程序之间进行交互
    
node中同步和异步如何理解
    node是单线程的，异步是通过一次次的循环事件队列来实现的
    同步则是说阻塞式的IO，在高并发环境会是一个很大的性能问题，所以同步一般只会在基础框架的启动时使用，
    用来加载配置文件，初始化程序。


哪些方法可以进行异步流程的控制？
    多层嵌套回调
    为每一个回调写单独的函数，函数里面再回调
    用第三方框架 async promise

怎样绑定node程序到80端口
    sudo
    apache/nginx代理
    操作系统的firewall iptables进行端口重定向

哪些方法可以让node程序遇到错误后自动重启
    runit 
    forever
    nohup npm start

怎样充分利用cpu
    一个cpu运行一个node实例

怎样调节node执行单元的内存大小
    --max-old-space-size
    --max-new-space-size来设置v8使用内存的上限

程序总是崩溃，怎样找出问题
    node --prof 查看哪些函数调用次数多
    memwatch和heapdump 获得内存快照进行对比，查找内存溢出

防止程序崩溃
    try-catch-finally
    EventEmitter/Stream error事件处理
    domain统一控制
    jshint静态检查
    jasmine/mocha进行单元测试

mongodb常用的优化措施
    索引 分区

redis支持哪些功能
    set/get
    hset/hget
    publish/subscribe
    expire


    


```