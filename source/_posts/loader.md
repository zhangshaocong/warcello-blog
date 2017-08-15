---
title: 8.Webpack Loader之css-loader,row-loader,file-loader
date: 2017-08-02 09:08:49
tags: Webpack
categories: Webpack,前端
---


今天讲讲图片url如何通过webpack编译的

1.css-loader的中禁用url处理

```js
{
	test:/\.s[ac]ss$/,
	use:ExtractTextPlugin.extract({
		
		use:[
			{
				loader:'css-loader',
				options:{ url:false },
			},
		],
		fallback:'style-loader',
		}),
},
```

这样在运行后webpack就不会对url中的内容进行处理

2.row-loader

 安装
 
```
npm install --save-dev raw-loader

```

使用

```
{
   test: /\.png|jpg|gif$/,
   use: 'raw-loader'
}
```
这样就会在dist目录下生成一张.png的图片

3.file-load 生成文件

安装

```
npm install --save-dev file-loader

```
使用


```
{
	test: /\.(png|jpg|gif)$/,
	loader: 'file-loader',
	options: {
		name: 'images/[name].[hash].[ext]'
	}

},
```
这里说一下options里的name就是指生成的文件名，hash指生成带hash的文件名，ext指文件后缀


