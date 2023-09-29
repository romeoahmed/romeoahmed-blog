---
title: "使用 Hugo + Github Actions + Cloudflare Pages 搭建你的第一个博客"
slug: "first-blog"
date: 2023-08-28T21:45:21+08:00
toc: true
draft: false
readingTime: true
comments: true
categories: ["教程"]
tags: ["博客", "Hugo", "cloudflare"]
keyword: ["Hugo", "Github", "Cloudflare", "博客", "第一"]
---

本教程将指导你使用 Hugo 静态网页生成器、Github Actions 自动更新主题以及 Cloudflare Pages 部署博客。我们将使用 Hugo 的 [stack](https://themes.gohugo.io/themes/hugo-theme-stack/) 主题。

## 安装 Hugo

首先，你需要安装 Hugo。请访问 [Hugo 官方网站](https://gohugo.io/getting-started/installing/) 获取安装说明。

## 创建新的 Hugo 网站

在安装 Hugo 后，打开终端并运行以下命令创建一个新的 Hugo 网站：

```bash
hugo new site my-blog
cd my-blog
```

## 添加 stack 主题

接下来，我们将添加 stack 主题。在终端中运行以下命令：

```bash
git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/stack
```

然后，在 `config.toml` 文件中添加以下内容以启用 stack 主题：

```toml
theme = "stack"
```

## 创建内容

现在，你可以开始创建博客内容。运行以下命令创建一篇新文章：

```bash
hugo new posts/my-first-post.md
```

编辑 `content/posts/my-first-post.md` 文件，添加你的文章内容。

启动 Hugo 服务器：

```bash
hugo server -D
```

现在你可以在 `http://localhost:131` 预览网站。

## 部署到 Cloudflare Pages

首先，你需要在 Github 上创建一个新的仓库。将你的 Hugo 网站推送到新创建的 Github 仓库。

接下来，访问 [Cloudflare Pages](https://pages.cloudflare.com/)，登录并点击 "Create a new project"。选择你刚刚创建的 Github 仓库。

在 "Set up builds and deployments" 部分，提供以下信息：

- Production branch: `main`（或你的仓库的默认分支）
- Build command: `hugo --gc --minify`
- Build directory: `public`

点击 "Save and Deploy"。Cloudflare Pages 将安装 Hugo 并构建你的网站。

部署完成后，你将收到一个 `*.pages.dev` 子域名，用于访问你的博客。

## 使用 Github Actions 自动更新主题

创建一个名为 `.github/workflows/update-theme.yml` 的新文件，并添加以下内容：

```yaml
name: Update theme

on:
  schedule:
    - cron: "0 0 * * *"

  workflow_dispatch:

jobs:
  update-theme:
    runs-on: ubuntu-latest

    permissions:
      contents: write
    
    steps:
      - uses: actions/checkout@v3

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"
          extended: true

      - name: Update theme
        run: git submodule update --remote --merge

      - name: Commit changes
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: "CI: Update theme"
```

这将创建一个 Github Actions 工作流，每天自动更新 stack 主题。

现在，你已经成功使用 Hugo、Github Actions 和 Cloudflare Pages 搭建了你的第一个博客。每次向 Github 仓库推送新的内容时，Cloudflare Pages 都会自动构建并部署你的博客。
