---
title: 12.Webpack img-loader
date: 2017-08-07 09:13:28
tags: Webpack
categories: Webpack,前端
---


 图片压缩
 
## 安装


```
$ npm install img-loader --save-dev
```

## 使用

```
module: {
  rules: [
    {
      test: /\.(jpe?g|png|gif|svg)$/i,
      use: [
        'url-loader?limit=10000',
        'img-loader'
      ]
    }
  ]
}
```


