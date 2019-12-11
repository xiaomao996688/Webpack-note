##安装babel
npm install --save-dev babel-loader @babel/core

module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
  ]
}
npm install @babel/preset-env --save-dev
{
  "presets": ["@babel/preset-env"]
}

webpack.config.js
```js
	{ test: /\.js$/, 
			exclude: /node_modules/,
			// babel-loader只是让webpack与babel进行通信
			 loader: "babel-loader" ,
			 options:[
			 	"presets": ["@babel/preset-env"]
			 ]
		},

````
安装了babel-loader
后发现打包的东西变大了
npm install --save @babel/polyfill

##使用了babelpli
rules:[
	{ test: /\.js$/, 
		exclude: /node_modules/,
		// babel-loader只是让webpack与babel进行通信
		 loader: 'babel-loader' ,
		 options:{
		 	"presets": [['@babel/preset-env'],{
		 		useBuiltIns: 'usage'
		 	}]
		 }
	},
这样可以减少打包的大小
```js
rules:[
{ test: /\.js$/, 
	exclude: /node_modules/,
	// babel-loader只是让webpack与babel进行通信
	 loader: 'babel-loader' ,
	 options:{
	 	"presets": [['@babel/preset-env'],{
	 		// 使用polyfill不是所有使用了es6或者es其他api都打包，只打包已经使用了
	 		// 按需引入
	 		useBuiltIns: 'usage'

	 	}]
	 }
}
```
babel-presets的配置
```
	{ test: /\.js$/, 
		exclude: /node_modules/,
		// babel-loader只是让webpack与babel进行通信
		 loader: 'babel-loader' ,
		 options:{
		 	"presets": [['@babel/preset-env'],{
		 		// 使用polyfill不是所有使用了es6或者es其他api都打包，只打包已经使用了
		 		useBuiltIns: 'usage'，
		 		targets: {
		 			// 如果大于67的版本就没有必要再使用babel和polyfill来转换成es5了
	        chrome: ">67"
	      }
		 	}]
		 }
	},
```
配置babel-polyfill
npm install --save-dev @babel/plugin-transform-runtime
npm install --save @babel/runtime
如果写 的是业务代码只需配置presets
```
			exclude: /node_modules/,
			// babel-loader只是让webpack与babel进行通信
			 loader: 'babel-loader' ,
			 options:{
			 	// "presets": [['@babel/preset-env'],{
			 	// 	// 使用polyfill不是所有使用了es6或者es其他api都打包，只打包已经使用了
			 	// 	useBuiltIns: 'usage'，
			 	// 	targets: {
		   //      chrome: ">67"
		   //    }
			 	// }]
			 	// babel-
			 		"plugins": [["@babel/plugin-transform-runtime",{
				 	"absoluteRuntime": false,
				 	// 如果把这个改成2还需安装一个2的包
	        "corejs": 2,
	        "helpers": true,
	        "regenerator": true,
	        "useESModules": false
			 	}]]
			 }

```
配置完babel文件后要在入口文件内引入babel/polyfill
import "@babel/polyfill";
### @babel/plugin-transform-runtime
会避免全局污染，
避免presets的问题与babel-polyfil

## 配置babel 的配置文件
.babelrc
```js
{
	  "plugins": [["@babel/plugin-transform-runtime",{
		 	"absoluteRuntime": false,
		 	// 如果把这个改成2还需安装一个2的包
      "corejs": 2,
      "helpers": true,
      "regenerator": true,
      "useESModules": false
	 	}]]
}
```

<!-- babel执行顺序，先执行下到上再执行从左到右 -->