---
title: 9.Webpack Plugs PurifyCSS
date: 2017-08-03 09:10:09
tags: Webpack
categories: Webpack,前端
---


此插件使用PurifyCSS从CSS中删除未使用的选择器,应该配合extract-text-webpack-plugin使用

没有任何CSS文件作为资产发布，这个插件什么都不做。您还可以使用文件插件将CSS文件放入输出文件夹，但强烈建议您使用Extract Text插件的PurifyCSS插件。

## 安装

```
npm i -D purifycss-webpack purify-css
```

## 使用

```js
const path = require('path');
const glob = require('glob');
const ExtractTextPlugin = require('extract-text-webpack-plugin');
const PurifyCSSPlugin = require('purifycss-webpack');

module.exports = {
  entry: {...},
  output: {...},
  module: {
    rules: [
      {
        test: /\.css$/,
        loader: ExtractTextPlugin.extract({
          fallbackLoader: 'style-loader',
          loader: 'css-loader'
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin('[name].[contenthash].css'),
    // Make sure this is after ExtractTextPlugin!
    new PurifyCSSPlugin({
      // Give paths to parse for rules. These should be absolute!
      paths: glob.sync(path.join(__dirname, 'app/*.html')),
      minimize:true,//代码压缩
    })
  ]
};
```

