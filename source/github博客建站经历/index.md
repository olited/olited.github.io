---
title: github 博客建站经历
date: 2024-10-17 02:11:19
---

## 第一篇文章, 时间不早了, 浅浅写写

1. 拥有一个 github 账号

1. 新建项目 名为 "{username}.github.io", 额外建立分支为 gh-pages

1. 本地上安装 hexo (或者其他博客网站模版)

1. hexo init 后提交到 github 上 sitting -> pages -> source -> actions 自己建立工作流程

1. pages.yml内容如下

   ```yaml
   name: Deploy GitHub Pages
   permissions:
     contents: write
   
   # 触发条件：在 push 到 main 分支后
   on:
     push:
       branches:
         - main
   # 任务
   jobs:
     build-and-deploy:
       # 服务器环境：最新版 Ubuntu
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v4
         - name: Use Node.js 21
           uses: actions/setup-node@v4
           with:
             # Examples: 20, 18.19, >=16.20.2, lts/Iron, lts/Hydrogen, *, latest, current, node
             # Ref: https://github.com/actions/setup-node#supported-version-syntax
             node-version: "21.7.2"
         - name: Build
           run: npm install && npm run build
   
         - name: Deploy to GitHub Pages
           uses: JamesIves/github-pages-deploy-action@v4.6.8
           with:
             ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
             REPOSITORY_NAME: litedit/litedit.github.io
             BRANCH: gh-pages
             FOLDER: public
   ```

1. 设置 sitting -> pages -> source -> Deploy from a branch, Branch 选择gh-pages, 使用根目录

1. 从此之后每次 push 到 main 分支都会执行任务, github action会自动将构建出来的 public 文件夹 push 到 gh-pages 分支中

1. 保存

注：写完 pages.yml 后报错不用管, 建立分支之后就行了