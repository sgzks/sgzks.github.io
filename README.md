# Jekyll 静态网站生成与 GitHub Pages 部署

## 项目简介

本项目是一个基于 Jekyll 的静态博客网站，用于《Jekyll 的静态网站生成与 GitHub Pages 部署》实验。

## 目录结构

```
.
├── _config.yml          # Jekyll 配置文件
├── _layouts/            # 模板文件目录
│   ├── default.html     # 默认模板（父模板）
│   └── post.html        # 文章模板（继承自 default）
├── _posts/              # 博客文章目录
│   └── 2024-01-01-example-post.md
├── assets/
│   └── css/
│       └── custom.scss  # SCSS 样式文件
├── index.md             # 首页
├── about.md             # 关于页
├── categories.md        # 分类页
└── .github/
    └── workflows/
        └── pages.yml    # GitHub Actions 部署配置
```

## 关键技术说明

### 1. Front Matter

Front Matter 是 Markdown 文件顶部的 YAML 配置区域，用于定义页面元数据：

```yaml
---
layout: post
title: "文章标题"
date: 2024-01-01
category: "技术教程"
tags: ["Jekyll", "教程"]
---
```

### 2. Liquid 模板继承

模板继承允许复用页面结构：

- `_layouts/default.html` - 基础模板，包含导航栏、页脚等公共部分
- `_layouts/post.html` - 文章模板，通过 `{% extends "default.html" %}` 继承基础模板

### 3. SCSS 变量与嵌套

SCSS 支持变量定义和嵌套语法：

```scss
$primary-color: #2c3e50;
$spacing-md: 1.5rem;

.site-header {
  background-color: $primary-color;
  
  .navbar {
    padding: $spacing-md;
  }
}
```

## 本地运行

```bash
# 安装依赖
bundle install

# 启动开发服务器
bundle exec jekyll serve

# 访问网站
# http://localhost:4000
```

## GitHub Pages 部署指南

### 1. 初始化 Git 仓库

```bash
git init
git add .
git commit -m "Initial commit"
```

### 2. 创建 GitHub 仓库

在 GitHub 上创建一个新仓库：
- 如果仓库名为 `username.github.io`，则网站会部署到 `https://username.github.io`
- 如果仓库名为其他名称（如 `jekyll-blog`），则网站会部署到 `https://username.github.io/jekyll-blog`

### 3. 配置 baseurl

**如果仓库名不是 `username.github.io`**，需要修改 `_config.yml`：

```yaml
baseurl: "/仓库名称"  # 例如："/jekyll-blog"
url: "https://username.github.io"
```

### 4. 推送到 GitHub

```bash
git remote add origin https://github.com/username/仓库名称.git
git branch -M main
git push -u origin main
```

### 5. 配置 GitHub Pages

1. 进入仓库的 **Settings** -> **Pages**
2. 在 **Source** 部分选择：
   - **Branch**: `gh-pages`
   - **Folder**: `/root`
3. 点击 **Save**

### 6. GitHub Actions 自动部署

本项目已配置 `.github/workflows/pages.yml`，每次推送到 `main` 分支时会自动：
1. 安装依赖
2. 构建 Jekyll 站点
3. 部署到 GitHub Pages

部署完成后，访问 `https://username.github.io/仓库名称` 即可查看网站。

## 实验报告要点

1. **Front Matter 的作用**：定义页面元数据，供模板引擎使用
2. **Liquid 模板继承**：实现代码复用，`post.html` 继承 `default.html`
3. **SCSS 变量与嵌套**：提高样式代码的可维护性
4. **GitHub Pages 部署流程**：本地开发 -> 推送代码 -> Actions 自动构建部署

## 参考链接

- [Jekyll 官方文档](https://jekyllrb.com/docs/)
- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [Liquid 模板文档](https://shopify.github.io/liquid/)