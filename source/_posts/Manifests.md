---
title: 11.Webpack Manifests
date: 2017-08-06 09:10:22
tags: Webpack
categories: Webpack,前端
---


我们可以成功地将（我们）捆绑的版块（hash）版本（哈希），但现在我们有一个新问题：如果文件哈希不断变化，我们如何在HTML中引用它？我们不能再硬编码路径了。而是让webpack生成一个manifest.json文件。这样，使用Ruby，PHP或者填空，我们可以读取这个文件并动态地确定并获取正确的哈希。


```js
function () {
			this.plugin('done',stats => {
				require('fs').writeFileSync(
					path.join(__dirname,'dist/manifest.json'),
					JSON.stringify(stats.toJson().assetsByChunkName)
					)
			})
		}
```

