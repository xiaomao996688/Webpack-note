## Loaders(装载机)
Out of the box,webpack only understands JavaScript and JSON files,Loaders allow webpack to process other types of files and convert(vt使转变vi转变) them into valid modules that can be consumed(adj.充满的) by your application and added to the dependency graph.
```
	Note that the ability to import any type of module,e.g .css files,is a feature specific to webpack and may not be supported by other bundlers or task runners.We feel this extension of the language is warranted(adj.担保的) as it allows developers to build a more accurate(adj.精确的) dependency graph.
```
At a high level,loaders have two properties in your webpack configurationL
1. The test property identifies which file or files should be transformed.
2. The use property indicates which loader should be used to do the transforming.
webpack.config.js
```js
const path = require('path')
modules.exports = {
	output:{
		filename: 'my-first-webpack.bundle.js'
	},
	module: {
		rules: [
			{test:/\.txt$/,use:'raw-loader'}
		]
	}
}
```
The configuration above has defined a rules property for a single module with two required properties:test and use.This tell webpack'compiler the following:

>"Hey webpack compiler,when you come across a path resolves to a '.txt' file inside of a require()/ import statement,use the row-loader to ransform it before you add it to the bundle."
```
	It is important to remember that when defining rules in your webpack config,you are defining them under module.rules and not rules. For your benefit,webpack will warn you if this is done incorrectly(adv.错误地;不适当地)

```
```
	Keep in mind that when using regx to match files,you may not quote(n,引文;语录;开价;引号v.引述;引用;举例说明;报价;) it.i.e /\.txt$/ is not the same as '/\.txt$' or "/\/txt$/". The former instructs webpack to match ang file that ends with .txt and the latter instructs(vt.指导,命令;通知;教授) webpack to match a single file with an absolute path .'txt';this is likely not your intention.s
```
You can check further customization when including loaders secation.

## loader
在webpack中的loader是有执行顺序的
是从右到做
从下到上
文件的结尾不是js就考虑使用loader,
不同的文件应该使用不同的文件loader
```js
	// 当webpack找不规则的时候在module里找
	module:{
		rules:[{
			test:/\.png$/,
			use:{
				loader:'file-loader'
			}
		}]
	}
url loader比file-loader的功能更加强大，所以可以使用url-loader代替file-loader
url-loader图片打包成了base64的图片
但是这样用不合理，因为这样就是图片太多太大都在js文件里
这样请求很慢。所以很小的图片可以用。
````

## 样式loader
style-loader
会把样式挂载到head标签中
css-loader整合在一起
## less和scss，stulys
打包SCSS文件还需要借助其他的loader
sass-loader与node-sass
node-sass安装失败的解决办法
```js
第一步
yarn add（npm install）css-loader style-loader sass-loader -D
第二步
　　npm：
npm config set sass-binary-site http://npm.taobao.org/mirrors/node-sass
yarn：
yarn config set sass-binary-site http://npm.taobao.org/mirrors/node-sass
然后yarn add（npm install） node-sass 

````
## 自动添加厂商前缀的loader
postcss-loader
配置postcss.config.js
文件
增加一个autoprefixer插件即可
在loader中添加postcss-loader插件

## css-loader的配置
```
			test:/\.scss$/,
			use:[
			'style-loader',
			{
				loader: 'css-loader',
				options:{
					importLoaders:2
				}
			},
			'sass-loader',
			'postcss-loader'
			]
		}]
```
## 模块化打包CSS
```
	// 也要引入下面2个loader
				loader: 'css-loader',
				options:{
					importLoaders:2，
					modules:true
				}
添加样式
import style from './index.scss'
img.classList.add(style.avatar);
```

## 打包字体文件
```js
{
		test:/\.(eot|ttf|svg))/,
		use:{
			loader:'file-loader'
		}
}
````
webpack 把css里处理，所以把css单独包

## stylus 
使用安装stylus
开发环境
npm i stylus stylus-loader
正则的时候会报错
{
	test: /\.styl(us)?$/,
	use: ['style-loader','css-loader',{loader:'postcss-loader', options:{ sourceMap: true}},'stylus-loader']
}
线上环境