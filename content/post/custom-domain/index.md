---
title: "为你的博客设置自定义域名并开启 CDN 加速"
slug: "custom-domain"
date: 2023-08-28T22:41:47+08:00
toc: true
draft: false
readingTime: true
comments: true
categories: ["教程"]
tags: ["博客", "域名", "cloudflare", "CDN"]
keyword: ["域名", "Cloudflare", "CDN", "博客"]
---

本教程将指导你如何为你的博客设置自定义域名并开启 CDN 加速。我们将使用以下服务：

- Cloudflare：提供DNS解析与CDN加速
- Cloudflare Pages：博客部署平台
- 域名注册商：Namesilo

## 注册域名

首先，你需要在域名注册商（如 Namesilo）注册一个域名。注册完成后，你将拥有一个独特的域名，例如：`yourdomain.com` 。

## 设置 Cloudflare

接下来，你需要创建一个 Cloudflare 账户并添加你的域名。按照 Cloudflare 的引导操作，将你的域名的 DNS 解析服务器更改为 Cloudflare 提供的服务器。

## 部署博客到 Cloudflare Pages

将你的博客代码部署到 Cloudflare Pages 。在部署过程中，你需要设置自定义域名。在 Cloudflare Pages 的设置页面，找到 `Custom Domains` 部分，添加你的域名 `yourdomain.com` 。

如果你成功将 DNS 解析服务器更改为 Cloudflare 提供的服务器，Cloudflare Pages 将自动添加 CNAME 记录并为你的博客启用 HTTPS 加密。

## 配置 SSL 证书

在 Cloudflare 的 SSL/TLS 设置页面，选择 `Full(strict)` 模式。这将启用 HTTPS 加密，确保你的博客访问安全。

## 测试访问

现在，你可以尝试访问你的博客，`https://yourdomain.com` 。如果一切正常，你将看到你的博客内容。

## 优化设置（可选）

你可以在 Cloudflare 中启用一些额外的设置，以优化你的博客性能和安全性，例如：

- 开启 `Auto Minify` 以压缩HTML、CSS和JavaScript文件
- 开启 `Brotli` 以进一步压缩传输的内容
- 配置 `Page Rules` 以实现更高级的缓存策略

完成以上步骤后，你的博客将使用自定义域名并通过 Cloudflare 提供的 CDN 加速访问。
