## HMR(HotMoudleReplacement)热模块替换
是webpack自带的模块，
配置webpack-devsrver即可
devServer:{
	//开启HMR
	hot:true,
	//如果HMR没有生效那么也不让浏览器刷新
	hotOnly:true
}
const webpack = require('webpack')
new webpack.HotModuleRelacementPlugin()
```
    "bundle": "webpack",
    "watch": "webpack --watch",
    "start": "webpack-dev-server",
    "middleware":"node server.js"
```
"start": "webpack-dev-server"打包没有生成dist目录
原因是因为没产生目录，原因把dist放在内存中了，从而提升性能。

### 不刷新页面加载
```
	hot:true,
		// 如果HRM没有生效，也不让浏览器刷新
		hotOnly:true
```
解决问题，不会重新刷新页面而重新加载页面样式
不会改动html的结构，方便调试css

js问题,引入了俩个模块，改变了一个模块，其他的模块也会刷新。
// 如果开启了HMR 
if(module.hot)
{
	// 就执行下面代码
	// 接受一个参数，一来
	// 如果number发生变化就会重新执行一次这个函数
	// css不用这个HMR实现
	// 一些特殊的文件，没有这个HMR需要自己写
	module.hot.accept('./number.js',()=>{
		document.body.remove(document.getElementById('number'))
		number()
	})
}

### HMR
当CSS样式改变的时候不会重新刷新页面，改变css以外的模块
只更改css的样式
当js文件更改的时候，会自动更新相应的模块，而不必去加载所有的摸块