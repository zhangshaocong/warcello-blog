---
title: 6.Webpack插件之sass-loader
date: 2017-07-29 09:05:14
tags: Webpack
categories: Webpack,前端
---


1.安装

```
npm install sass-loader node-sass webpack --save-dev
```

2.使用
在`webpack.config.js`中加入如下代码

```js
	{
		test:/\.s[ac]ss$/,
		use:['style-loader','css-loader','sass-loader']
	},
```
创建`main.scss`文件

```css
$primary:green;

body {
	background:$primary;
}
```

修改`main.js`将`main.scss`引入进去

```js
require('./main.scss');
```

运行`npm run dev`查看效果


[点击查看sass-loader原文文档](https://doc.webpack-china.org/loaders/sass-loader)

