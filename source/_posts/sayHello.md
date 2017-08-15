---
title:  2.Webpack Hello World
date: 2017-07-25 09:58:13
tags: Webpack
categories: Webpack,前端
---


## 创建项目

1.初始化项目

```
mkdir learn-webpack
cd learn-webpack
npm init -y
```
此时项目底下将有一个package.json文件   

2.npm安装webpack

```
//此命令是全局安装 
npm install webpack -g

```
此时 Webpack 已经安装到了全局环境下，可以通过命令行 webpack -h 试试。

通常我们会将 Webpack 安装到项目的依赖中，这样就可以使用项目本地版本的 Webpack

```
npm install webpack --save-dev

```

3.创建main.js文件并对改文件进行打包

main.js

```js
alert("hello world")

```

```
//全局安装使用这个方法打包
webpack src/main.js dist/bundle.js

//本地项目打包使用
node_modules/.bin/webpack src/main.js dist/bundle.js

```

4.创建index.html文件并将bundle.js引入

index.html   

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
<h1>Hello Wold!</h1>

<script src="dist/bundle.js"></script>
</body>
</html>

```

5.打开浏览器查看效果   

6.修改main的js后发现alert不对重新打包后恢复正常，总不能每次修改都重新编译吧，当然不会，webpack提供我们一个观察者模式。   

```
//全局安装使用这个方法打包
webpack src/main.js dist/bundle.js --watch

//本地项目打包使用
node_modules/.bin/webpack src/main.js dist/bundle.js --watch
```
此时再对文章修改之后就不用再打包了
我们在将这些命令优化一下，打开package.js
在script数组中修改如下

```
"scripts": {
    "build": "webpack src/main.js dist/bundle.js",
    "watch": "npm run build --watch"
  },
```
打开命令行工具运行
```
npm run watch
```
此效果跟直接运行`webpack src/main.js dist/bundle.js --watch`一致


 







