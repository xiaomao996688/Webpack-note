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