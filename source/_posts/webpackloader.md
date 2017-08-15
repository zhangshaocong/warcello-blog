---
title: 4.Webpack loader带代码转换
date: 2017-07-27 09:03:00
tags: Webpack
categories: Webpack,前端
---

loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！

## 创建css文件
我们在src文件夹下创建一个main.css文件

```css
body {
    background:yellow;
}
```
## 安装loader插件

```bash
npm install css-loader style-loader --save-dev
```
## 修改webpack.config.js

```js
module:{
    rules:[
        {
            test:/\.css$/,
            use:['style-loader','css-loader']
        }
    ]
}
```
## 运行`npm rum build`后查看浏览器效果

## 内联
可以在 import 语句或任何等效于 "import" 的方式中指定 loader。使用 ! 将资源中的 loader 分开。分开的每个部分都相对于当前目录解析。通过前置所有规则及使用 !，可以对应覆盖到配置中的任意 loader。
尽可能使用 module.rules，因为这样可以减少源码中的代码量，并且可以在出错时，更快地调试和定位 loader 中的问题。

```js
import Styles from 'style-loader!css-loader?modules!./styles.css';
```


