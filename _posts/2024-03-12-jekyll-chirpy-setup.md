---
title: Jekyll Chirpy 主题配置指南
date: 2024-03-12 01:00:00 +0800
categories: [博客搭建]
tags: [jekyll, github pages, chirpy]
---

# Jekyll Chirpy 主题配置指南

本文记录了如何在 GitHub Pages 上搭建和配置 Jekyll Chirpy 主题的完整过程。

## 环境要求

- Ruby >= 3.2
- Node.js
- Git

## 主题版本

- jekyll-theme-chirpy ~> 7.2
- jekyll ~> 4.3

## 基础配置

### Gemfile 配置


这里部署的时候，推荐官方地址，如果是开发，用清华或者阿里的源，会更快
```ruby
source "https://rubygems.org"

gem "jekyll", "~> 4.3"
gem "jekyll-theme-chirpy", "~> 7.2"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-sitemap"
  gem "jekyll-paginate"
  gem "jekyll-seo-tag"
  gem "jekyll-archives"
  gem "jekyll-redirect-from"
end

platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
```

### _config.yml 关键配置

```yaml
theme: jekyll-theme-chirpy
baseurl: ""
lang: zh-CN
timezone: Asia/Shanghai

title: 你的博客标题
tagline: 副标题
description: >-
  网站描述

url: "https://username.github.io"

github:
  username: your-github-username

social:
  name: 你的名字
  email: your-email@example.com
  links:
    - https://github.com/username

avatar: /assets/img/sample/avatar.jpg

toc: true

paginate: 10
```

## GitHub Actions 自动部署配置

### .github/workflows/main.yml

```yaml
name: Build and Deploy to GitHub Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: write
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: "3.2"
          bundler-cache: true
      - name: Install Dependencies
        run: bundle install
      - name: Build Site
        run: bundle exec jekyll build
        env:
          JEKYLL_ENV: production
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_site
          publish_branch: gh-pages
          force_orphan: true
```

### .gitignore 配置

```
# Bundler cache
.bundle
vendor
Gemfile.lock

# Jekyll cache
.jekyll-cache
.jekyll-metadata
_site/

# RubyGems
*.gem

# NPM dependencies
node_modules
package-lock.json

# IDE configurations
.idea
.vscode/*
!.vscode/settings.json
!.vscode/extensions.json
!.vscode/tasks.json

# Misc
_sass/vendors
assets/js/dist
```

## 部署流程

1. 源代码推送到 main 分支
2. GitHub Actions 自动构建网站
3. 构建结果自动推送到 gh-pages 分支
4. GitHub Pages 从 gh-pages 分支部署网站

## GitHub Pages 设置

1. 进入仓库的 Settings > Pages
2. 在 "Build and deployment" 部分：
   - Source: 选择 "Deploy from a branch"
   - Branch: 选择 "gh-pages" 和 "/(root)"

## 常见问题解决

### feed.xml 冲突

如果遇到 feed.xml 冲突问题，在 _config.yml 中配置：

```yaml
feed:
  path: feed.xml
```

### SASS 编译错误

确保使用最新的 SASS 语法：
- 使用 `@use` 替代 `@import`
- 使用 `math.div()` 替代 `/` 运算符

## 本地开发

```bash
bundle install
bundle exec jekyll serve --livereload
```

访问 http://127.0.0.1:4000/ 预览网站。

## 注意事项

1. 确保 GitHub 仓库名称格式为 `username.github.io`
2. 提交代码前先在本地预览
3. 修改配置文件后需要重启 Jekyll 服务
4. 静态资源文件放在 assets 目录下
5. 文章放在 _posts 目录，文件名格式为 `YYYY-MM-DD-title.md`

## 参考链接

- [Chirpy 主题文档](https://chirpy.cotes.page/)
- [Jekyll 文档](https://jekyllrb.com/docs/)
- [GitHub Pages 文档](https://docs.github.com/en/pages) 