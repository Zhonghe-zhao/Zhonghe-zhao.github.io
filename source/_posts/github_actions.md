---
title: 发布博客出现的问题
---

每一次用push推送到githubpage都会出现构建部署错误 我问了一下ai原因 这才有点明白到底是为什么

#### 原因

为什么会有这种差异？
GitHub Pages 和 本地环境的差异：

在本地执行 hexo d 时，你的本地环境会根据 package.json 中的依赖来安装所有的主题和插件，确保所有必要的资源都存在。
但是 GitHub Pages 仅仅依赖仓库中已经推送的文件（通常是 public/ 文件夹和 ._config.yml），它不会自动运行 npm、yarn 或 pnpm 来安装依赖。换句话说，GitHub Pages 并不会在部署过程中安装缺少的主题或插件。
依赖没有正确推送：

你在本地运行 hexo d 时，可能已经正确地安装了 butterfly 主题，并且该主题存在于本地的 _config.yml 中和 node_modules 文件夹中。
然而，在推送到 GitHub 上时，你没有将 node_modules 中的 butterfly 主题或相关配置文件推送到 GitHub 仓库。GitHub Pages 需要能够访问这些主题文件，而它不会在部署过程中下载和安装这些依赖。
GitHub Pages 配置问题：

如果你直接使用 GitHub Pages 作为部署平台，GitHub 并不会自动安装你的 Hexo 依赖，因此它不能像本地环境一样找到 butterfly 主题。
GitHub Pages 需要使用一个可以通过静态文件夹来部署的版本，而 Hexo 本地运行时通常会将主题内容放在 node_modules 中，这些内容并不会自动推送到 GitHub，除非你特别将它们包含在仓库中。

#### 解决方法

使用github-actions
并且在google查找到的方法添加 .nojekyll文件 让github站点不适用jekyll
~~~
name: Hexo Deploy

on:
  push:
    branches:
      - main  # 监听主分支的推送

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Install dependencies
        run: |
          npm install

      - name: Generate and Deploy
        run: |
          hexo generate
          hexo deploy
        env:
          HEXO_DEPLOY_PATH: ${{ secrets.HEXO_DEPLOY_PATH }}  # 设置部署路径
~~~
