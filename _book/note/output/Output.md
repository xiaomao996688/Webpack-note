## Output
The output property tell webpack where emit the bundles it creates and how to name these files.It default to ./dist/main.js for the main output file and to the ./dist folder for any other generated file <br>
You can configure this part os the process by specifying an output field in your configuration: <br>
webpack.config.js
```js
const path = require('path')
module.exports ={
	entry:'./path/to/my/entry/files.js',
	output:{
		path:path.resolve(__dirname,'dist'),
		filename:'my-first-webpack.bundle.js'
	}
}
```
In the example above,we use the output.filename and the output.path properties to tell webpack the name of our bundle and where we want it to be emitted to(它被释放).In case you're wondering about the path module being imported at the top,it is a core Node.module that gets used to mainpulate(vt操作;操纵;巧妙地处理;篡改) file pahts;
> The output property has many more configurable features.If you want to learn about the concepts behing it,you can read more in the output section.