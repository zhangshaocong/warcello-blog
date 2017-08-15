---
title: 10.clean-webpack-plugin
date: 2017-08-04 09:11:23
tags: Webpack
categories: Webpack,前端
---

一个webpack插件，在构建之前删除你的构建文件夹

## 安装


```
npm i clean-webpack-plugin --save-dev
```

## 使用

```js
const CleanWebpackPlugin = require('clean-webpack-plugin'); //使用
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins
const path = require('path');

//使用
let pathsToClean = [
  'dist',
  'build'
]

//使用
let cleanOptions = {
  root:     '/full/webpack/root/path',
  exclude:  ['shared.js'],
  verbose:  true,
  dry:      false
}

// sample WebPack config
const webpackConfig = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        loader: 'babel-loader'
      }
    ]
  },
  plugins: [
    new CleanWebpackPlugin(pathsToClean, cleanOptions),//使用
    new webpack.optimize.UglifyJsPlugin(), 
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
}
Paths
```

