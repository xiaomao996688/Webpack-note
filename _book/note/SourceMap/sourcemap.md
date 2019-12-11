## mode
在development模式已经默认配置了
sourceMap
## 配置关掉sourceMap
devtool:'none',
## sourceMap
告诉我们源代码哪里出错了而不是告诉打包结束后的代码哪里 有问题<br>
sourceMap它是一个映射关系,他知道dist目录下main.js文件96实际上对应的是src目录下index.js文件中的第一行。
## 使用sourceMap
把devtool:'source-map'
 就可以知道是哪里错了
## inline-source-map
devtool:'inline-source-map'
当使用inline-source-map的时候
会main.js.map的会打包放入js文件中
##cheap-inline-source-map
devtool:'cheap-inline-source-map'
当代码量很大的时候，正好代码出错了。
cheap会告诉代码到底在那里一行出错了。
这样比较耗性能。
如果写了cheap只针对业务文件。不会管第三方模块的问题
比如说loader，或者plugin。
如果想让cheap管第三方模块
可以使用
cheap-module-eval-source-map
## eval
打包速度最快的方式。
一样可以帮我们把错误定位到哪里。
打包后的文件没有任何map文件或者base64.
会形成eval()来解析
## cheap-module-eval-source-map
推荐使用
这种方式打包速度比较快。
这种方式报错也比较全面。
## 线上使用
mode: 'production'
devtool:'cheap-module-source-map'
##开发使用
mode:'development'
devtool:''

## 解决问题
如果代码出错了只知道打包出来的代码是第几行错了。
但是如果使用了sourcemap会把错误与源文件做一个映射知道原文件代码在那里错了
## source-map
会生成一个.map 文件
## inline
会把生成的.map文件合并到打包生成的文件之中。
##cheap
1. 只提示第几行出错了,不提示几列出错了
2. 只负责业务的代码出错，不管module出错的代码

## module
如果 module出错会指出module里的代码哪里错了。
## eval 执行方式
通过eval的方式对代码进行打包。
## souceMap的原理。