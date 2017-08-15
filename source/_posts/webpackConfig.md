---
title: 3.Webpack 配置文件
date: 2017-07-26 09:01:41
tags: Webpack
categories: Webpack,前端
---

根据文档描述，webpack在执行的时候，除了在命令行传递参数，还可以通过制定参数执行。默认情况下，会搜索当前目录的webpack.config.js文件。这个文件是一个 node.js 模块，返回一个 json 格式的配置信息对象，或者通过 --config 选项来指定配置文件

## 创建webpack.config.js
继续我们的项目，在根目录下创建webpack.config.js文件并加入一下内容

```js
var webpack = require('webpack');

module.exports = {
	entry: './src/main.js',
	output: {
		path: __dirname+'/dist',
		filename: 'bundle.js'
	}
}
```
打开命令行运行 `webpack` 并查看效果
这里需要注意一下路径问题，output中的path必须是绝对路径不能使用相对路径否则会报错

## 修改package.js
继续修改package.js将scripts换成如下

```js
"scripts": {
    "build": "webpack",
    "watch": "npm run build --watch"
  },
```
运行`webpack`查看效果





