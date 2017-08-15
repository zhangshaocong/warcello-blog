---
title: 5.Webpack 插件
date: 2017-07-28 09:04:15
tags: Webpack
categories: Webpack,前端
---


插件可以完成更多 loader 不能完成的功能。

插件的使用一般是在 webpack 的配置信息 plugins 选项中指定。

接下来我们演示一下代码压缩这个插件

## 1.修改`webpack.config.js`,添加plugins:

```js
plugins: [

		new webpack.optimize.UglifyJsPlugin()
		
	]

```
然后运行`npm run build`查看效果

## 2.这么运行之后发现代码压缩成一行了，不利于查看，现在我们把这个改一下，让他在开发环境压缩代码，在本地环境不进行压缩

修改`webpackage.config.js`


```js
var webpack = require('webpack');
var path = require('path');

module.exports = {
	entry: './src/main.js',
	output: {
		path:  path.resolve(__dirname,'./dist'),
		filename: 'bundle.js'
	},
	module:{
		rules:[
			{
				test:/\.css$/,
				use:['style-loader','css-loader']
			}
		]
	},
	plugins: [
		
	]
	
};
if (process.env.NODE_ENV == 'production') 
{
	module.exports.plugins.push(
		new webpack.optimize.UglifyJsPlugin()
		);
}

```
修改`package.json`

```json
"scripts": {
    "dev": "webpack",
    "production": "NODE_ENV=production webpack",
    "watch": "npm run build --watch"
  },

```
最后我们可以分别运行`npm run dev`,`npm run production`查看生成的js








