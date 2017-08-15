---
title: 7.Webpack插件ExtractTextWebpackPlugin
date: 2017-08-01 09:07:45
tags: Webpack
categories: Webpack,前端
---


它会将所有的入口 chunk(entry chunks)中引用的 *.css，移动到独立分离的 CSS 文件。因此，你的样式将不再内嵌到 JS bundle 中，而是会放到一个单独的 CSS 文件（即 styles.css）当中。 如果你的样式文件大小较大，这会做更快提前加载，因为 CSS bundle 会跟 JS bundle 并行加载。

## 1.安装

```
# 对于 webpack 3
npm install --save-dev extract-text-webpack-plugin
```
## 2.用法

```js
//webpack.config.js头部引入
var ExtractTextPlugin = require("extract-text-webpack-plugin");

module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: "css-loader"
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin("styles.css"),
  ]
}
```
## 3.修改文件名
`filename` 参数可以是 `Function`。它通过 `getPath` 来处理格式，如 `css/[name].css`，并返回真实的文件名，你可以用 `css` 替换 `css/js`，你会得到新的路径 `css/a.css`。


```js
entry: {
		app:[
			'./src/main.js',
			'./src/main.scss',
		]

	},
	output: {
		path:  path.resolve(__dirname,'./dist'),
		filename: '[name].js'
	},
	module:{
		rules:[
			{
				test:/\.s[ac]ss$/,
				use:ExtractTextPlugin.extract({
					use:['css-loader','sass-loader'],
					fallback:'style-loader',
					}),
			},
		]
	},
	plugins: [
		new ExtractTextPlugin('[name].css'),
		
	]
	
};
```
## 4.LoaderOptionsPlugin
loader-options-plugin 和其他插件不同，它用于将 webpack 1 迁移至 webpack 2。在 webpack 2 中，对 webpack.config.js 的结构要求变得更加严格；不再开放扩展给其他的 loader/插件。webpack 2 推荐的使用方式是直接传递 options 给 loader/插件（换句话说，配置选项将不是全局/共享的）。

不过，在某个 loader 升级为依靠直接传递给它的配置选项运行之前，可以使用 loader-options-plugin 来抹平差异。你可以通过这个插件配置全局/共享的 loader 配置，使所有的 loader 都能收到这些配置。

简单说就是格式转化转换成webpack能适配的代码格式（目前只是自己的理解）

用法直接在`plugins`数组中加入

```js
new webpack.LoaderOptionsPlugin({
      minimize: true,
    })
```
## 5.本节`webpack.config.js`源代码如下

```js
var webpack = require('webpack');
var path = require('path');
var ExtractTextPlugin = require("extract-text-webpack-plugin");
var inProduction = (process.env.NODE_ENV == 'production');

module.exports = {
	entry: {
		app:[
			'./src/main.js',
			'./src/main.scss'
		]

	},
	output: {
		path:  path.resolve(__dirname,'./dist'),
		filename: '[name].js'
	},
	module:{
		rules:[
			{
				test:/\.s[ac]ss$/,
				use:ExtractTextPlugin.extract({
					use:['css-loader','sass-loader'],
					fallback:'style-loader',
					}),
			},
		]
	},
	plugins: [
		new ExtractTextPlugin('[name].css'),
		new webpack.LoaderOptionsPlugin({
			  minimize: inProduction,
			})
	]
	
};
if (inProduction) 
{
	module.exports.plugins.push(
		new webpack.optimize.UglifyJsPlugin()
		);
}

```
## 6.最后

```
npm run dev //代码未压缩
npm run production  //代码已压缩
```




