## Plugins 
While loaders are used to transform certain types of modules,plugins can be leveraged(施加影响) to perform a wider range of task like bundle optimization(最佳的),asset(n.资产;优点;有用的东西;有利条件) management and injection of environment variables.
随着loader被使用去转变包含的模块类型，插件能影响应用去执行像最佳打包广泛的任务,资源管理和环境变量注入。
> Check out the plugin interface and how to use it to extends(vt&vi延伸；扩大) webpack's capabilities(n.性能,功能,能力)
In order to use a plugin, you need to require() it adn add it to the plugins array.Most plugins are customizable(adj.可定制的) through options.Since you can use a plugin multiple times in for different purposes(n.目的;意志v.打算;企图), you need to create an instance of it by calling it with the new operator.
```js
modules.exports = {
	modules:{
		rules:[
			{test:/\.txt$/,use:'raw-loader'}
		]
	},
	plugins:[
		new HtmlWebpackPlugin({template:'./src/index.html'})
	]
}
```
In the example above,the html-webpack-plugin generates an HTM file for your application by injecting automatically all your generated bundles.
> There are many plugins that webpack provides out of the box!Check out the list of plugin.
Using plugins in your webpack config is straightforward(adj.简单的;坦率的;明确的;adv.直截了当地;坦率地).However,there are many use cases that are worth further exploration.Learn more about them here.
## plugin
htmlWebpackPlugin 会在打包结束后，自动生成一个html文件，并把打包生成的js自动引入到这个html文件中。
## cleanwebpackplugin
会帮助在打包的时候先请客dist目录下的文件然后再进行打包
npm i clean-webpack-plugin
new CleanWebpackPlugin(['dist']
会在打包之前被运行清空dist的目录下的文件
## plugin配置方法
```js
	plugins:[new HtmlWebpackPlugin({
		template:"src/index.html"
	}),new CleanWebpackPlugin(['dist'])]
```

## 常用模块
CommonsChunkPlugin已经废弃在webpack4
splitChunks: 自动进行模块分割
- new chunk 可以被分享和模块是来自 node_modules文件加
- new chunk 将大于30kb(在压缩之前before min+gz)
- 最大数量的并行请求加载块时对需求会降低或等于5
- 最大数量的并行请求初始页面加载将低于或等于
```js
splitChunks: {
	chunk: "async",
	minSize: 30000, //默认模块大小
	minChunks: 1, //在分割之前分享一个模块的最小数量
	maxAsyncRequests: 5,//在入口点并行请求的最大数量
	maxInitialRequests: 3,// 最大请求数量的一个入口点
	automaticNameDelimiter: '~', //vendors~main.js
	name: true,//控制分割模块的选项明吃，设置为true自动的选一个名字作为key，否则传递一个函数或者字符串
	// 创建一个共享模块，包括代码分享的入口点
	cacheGroups: {
		verndrs: {
			test: /[\\/]node_modules[\\/]/,
			priority: -10 //缓存优先级
		}
	},
	default: {
		minChunks: 2,
		priority: -20,
		reuseExistingChunk: true
	}
}

````
```js
  optimization: {
    minimizer: [new optimizeCss({})],
    // 提取公共加载的块 其他模块内容改变时 公共加载模块不用改变 可以起到缓存作用
    runtimeChunk: true,
    splitChunks: {
      // 设置公共块的名称 可以是函数 || 字符串
      // name: 自定义函数名
      name: true,
      minSize: 1,
      // 定义分隔符
      automaticNameDelimiter: '-',
      cacheGroups: {
        vendors: {
          test: /[\\/]node_modules[\\/]/,
          priority: -3,
          chunks: "initial",
        },
        common: {
          // 控制缓存组选择的模块 省略它选择所有模块
          test: /[\\/]node_modules[\\/]/,
          priority: -4,
          chunks: "async",
          minChunks: 2,
          reuseExistingChunk: true,
        },
        reactBase: {
          name: 'reactBase',
          // 控制此缓存组选择的模块 省略它选择所有模块
          // module.context: 当前模块的路径
          test: (module) => {
            return /[\\/]vue|vue-router|vue-loader[\\/]/.test(module.context);
          },
          chunks: 'initial',
          priority: 10,
        },
        styles: {
          // module: 模块信息 module.context 该模块的路径
          // chunk: 打包的每个文件的信息 chunk.name 文件名
          name (module, chunk) {
            return `../css/${chunk[0].name}`
          },
          test: /\.css$/,
          chunks: 'all',
          enforce: true
        },
      }
    },
  },

```