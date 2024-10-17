# 主分支用于推送静态文件到 gh-pages 分支



## Front-matter 可编写内容

```yaml
---
title: 文章标题
tags:							   # 标签, 同分类有两种写法, 这是第一种
	- Hexo
	- ...
categories:[a,b]					# 分类, 同标签有两种写法, 这是第二种

index_img: /img/example.jpg			 # 首页图, 可使用外链(绝对路径), 如果default_index_img 和 index_img 都为空, 则不显示图片
banner_img: /img/example.jpg		 # 文章顶部大图 (背景图)
date: 0000						    # 日期
hide: true						    # 是否隐藏该文章, 不在首页和其他归档分类页里展示
archive: true                         # 不在首页展示, 仅在归档分类页里展示, 与上一项可能冲突
sticky: 100						    # 该值越大文章就越靠前, 用于实现置顶效果, 缺省则默认排序
comment: 'valine'					# 启用评论, 设置为 false 禁用评论
---
# 以下是文章内容...
```






注意: clone 该仓库后直接使用 hexo 可能会显示:

(node:16704) [DEP0040] DeprecationWarning: The \`punycode\` module is deprecated. Please use a userland alternative instead.
(Use \`node --trace-deprecation ...\` to show where the warning was created)


此时应该修改 node_modules\markdown-it\lib\index.js 中的源码
将其中的
```js
const punycode = require('punycode');
```
改为
```js
const punycode = require('punycode/');
```