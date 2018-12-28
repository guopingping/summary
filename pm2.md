pm2

```
pm2
    是带有负载均衡的node进程管理工具，用来简化很多node应用管理的繁琐任务。
如性能监控、自动重启、负载均衡等，使用简单。

    当你要把独立代码利用全部的服务器上的所有cpu，并保证进程永远活在，
    0秒的重载，pm2是完美的。

    主要特性：
        内建负载均衡（使用Node cluster集群模块）
        后台运行
        0秒停机重载，维护升级的时候不需要停机
        具有Ubuntu和CenOS的启动脚本
        停止不稳定的进程 避免无限循环
        控制台检测
        提供HTTP API
        远程控制和实时的接口API（Nodejs模块，允许和PM2进程管理器交互）

    npm install -g pm2

    pm2 start --watch

        --watch：监听应用目录的变化，一旦发生变化，自动重启。
        -i --instances：启用多少个实例，用于负载均衡
        --ignore-watch：排除监听的目录/文件
        -n --name：应用的名称，查看应用信息的时候可以用到
        -o --output <path>：标准输出日志文件的路径
        --e --error <path>：错误输出日志文件的路径

    pm2 start test.js --name my-test
            命名进程
    
    重启
        pm2 restart test.js
            pm2同时杀死并重启所有进程，短时间内服务不可用
        pm2 reload
            pm2逐个重启所有进程，但始终保持至少一个进程在运行
    停止
        pm2 stop app_name/进程id
        pm2 stop all     停止所有应用

    pm2 stop 0
        停止指定的进程
    pm2 restart 0
        重启指定的进程
    pm2 startup 0 
        产生init脚本，保存进程活着
    pm2 web
        允许健壮的computer API endpoint
    删除
        pm2 delete
    pm2 delete 0
        杀死指定的进程
    

    pm2 list
        获取应用的名字 显示所有进程状态
    pm2 monit
        监视所有进程状态
    pm2 describe 0
        查看某个进程的信息
    
    日志
        pm2 logs <app_name|all>

    pm2 show <name>
        查看某个进程下的日志地址

    pm2 start test.js -i max
        根据有效的CPU数目启动最大进程数目
    pm2 start test.js -i 3
        启动3个进程
    pm2 start text.js -x 
        用fork模式启动test.js，而不是使用cluster
    pm2 start test.js -x -- -a 23
        用fork模式启动test.js并且传递参数（-a 23)
    pm2 start test.js --name serverone 
        启动一个进程并把它命名为serverone
    pm2 stop serverone
        停止serverone进程
    pm2 start app.json
        启动进程，在app.json里设置选项
    

```