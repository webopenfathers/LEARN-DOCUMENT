# 💘 符号说明

🌟 常见重要   

🌛 需要有印象的

 

# 💘 项目区域

# 🌟 exports、module.exports



# 🌟 process

node全局变量

cwd 写接口用获取命令执行路径

argv 写npm -g脚本用 获取命令参数

env express源码、还有vue接口封装用  获取用户环境信息  

> ！！！ vue中主要用来获取用户配置文件信息 比如开发环境和线上环境接口地址









# 💘 面试区域

# 🌛  npm、yarn区别

````
相同点：都是用户下载第三方模块
不同点：主要说旧版本 现在差不多
npm5.x之前 没有锁定版本机制 后来才出了package-lock.json
npm5.x之前 没有离线缓存
npm是官方自带的，yarn是Facebook的
````





- 题目2：谈谈你对express、koa2、egg框架的理解

```
相同点：都是基于http模块封装的前端框架
不同点：主要是框架思想和语法上
1 express是callback  慢慢淘汰中 MVC框架
2 koa2 aysnc、await 升级版本   MVC框架
3 egg 是基于koa2的升级版  增加了很多后端思想，主要用户写接口；安全、单元测试、服务层、中间件。
```

- 题目3：谈谈你对websocket的理解

> ```
> 它是全双工通讯协议，客户端和服务端可以同时推送数据。
> 之前我做项目的时候，图 表就是使用的websocket实现的
> 还有聊天项目。
> ```

- 题目4：websocket怎么用 

> ```
> # jq怎么用
> 1引入jq库
> 2通过$.get/post/ajax发送请求
> 
> # websocket
> 1 引入socket.io库
> 2 创建socket对象    const socket = io()
> 3 使用emit发送数据，使用on接受数据
> ```



- 题目5：谈谈你对中间件的理解，有哪些中间件？

> 就是一个路由，来拦截请求 过滤数据  之后交给后面处理
>
> app.use  拦截所有请求   过滤加数据 token 解析token   next()



- 题目6：关乎token  最重要

> token作用：保证接口安全  加密
>
> token如何生成：利用jwt技术
>
> token生命周期：2小时，token里面存储了用户编号、生命周期等  后期请求后端利用自定义中间件过滤判断 当前时间 大于 存储时间 代表过期了！！！

- 等  
- 其他的：

```
tpc和udp区别
TCP的3次握手
TCP的4次挥手 
js是单进程还是多进程如何保证性能（后面说）
node是单进程还是多进程，如何保证性能 （后面都）
event loop （后面说）
```

 

