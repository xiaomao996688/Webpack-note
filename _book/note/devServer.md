## webpack --watch
会监听文件更新了会自动的进行打包。
这样的方式还是要刷新浏览器不够好
## devServer
```
	devServer:{
		//这个服务器要放在哪个文件夹下
		contentBase:'',
		//open会自动打开浏览器然后自动访问服务器地址
		open:true,
		//如果用户访问'/api'这个地址的话也就是
		//http://localhost:8080/api这个路径会被自动代理到
		//http://localhost:3000这个地址
		proxy:{
			'/api':'http://localhost:3000'
		},
		//默认服务开启的地址是localhost:8080
		port:8080,
			// 开启HMR
		hot:true,
		// 如果HMR没有生效，也不让浏览器刷新
		hotOnly:true
	},
```
不但会监听文件更新会自动打包
还会自动更新浏览器
好处，发生ajax请求要求必须使用http请求，如果使用
文件则不会发送请求