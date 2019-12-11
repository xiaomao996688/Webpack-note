## Entry(入口) 
An entry point indicates(表明) which module webpack should use to begin building out its internal(adj.内部的;体内的;本身的;内心的;本校生) dependency graph. webpack will figure out which other modules and libraies that point depends on(dirctly and indirectly).
入口点 模块webpack应该去使用去开始构建一个在它的内部的依恋关系图外面的表明 。webpack将会解决在其他模块和库依赖点的外面。<br>
By default its value  ./src/index.js,but you can specify a different(or multiple entry pinots) by configuring the entry property in webpack configuration.For example:
通过默认它的值./src/index.js,但是你能详细的一个不同(或者多个入口点)通过配置这个entry的数学在webpack配置。列如：

```js
	module.exports ={
		entry: './path/to/my/entry/file.js'
	}
```
## Entry
```js

entry:{
	// 默认打包出来的文件是main.js，key value相对应，如果不在webpack中output中修改
	main:'./src.index.js',
	sub:'./src.index.js'
}
```
```js
output:{
		filename:'[name].js',
		path:path.resolve(__dirname,'dist')
},
这样配置的时候就可以打包出多个文件的名字
```

```js
	output:{
		publicPath:'http://cdn.com.cn',
		filename:'[name].js',
		path:path.resolve(__dirname,'dist')
	},
<script type="text/javascript" src="http://cdn.com.cn/main.js"></script><script type="text/javascript" src="http://cdn.com.cn/sub.js"></script>
```
