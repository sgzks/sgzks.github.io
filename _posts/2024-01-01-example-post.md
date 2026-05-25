---
layout: post
title: "Jekyll 静态网站生成入门教程"
date: 2025-05-17
category: "技术教程"
tags: ["Jekyll", "静态网站", "GitHub Pages", "Web开发"]
author: "第七组：张静火,王翼龙,厉传禹,张祎涵,王子潭"
---

## 什么是 Jekyll

Jekyll 是一个简单的博客形态的静态网站生成器。它使用 Markdown 来撰写内容，通过 Liquid 模板引擎来构建页面布局，最终生成静态 HTML 文件。

## Jekyll 的核心概念

### Front Matter

Front Matter 是位于 Markdown 文件顶部的一段 YAML 配置区域，用三条短横线 `---` 包裹。它用于定义页面的元数据，如标题、日期、分类等。

{% raw %}
```yaml
---
layout: post
title: "文章标题"
date: 2024-01-01
category: "技术教程"
tags: ["Jekyll", "教程"]
---
```
{% endraw %}

### Liquid 模板引擎

Liquid 是 Jekyll 默认使用的模板引擎，它允许在 HTML 文件中插入动态内容。

下面列举 Liquid 的几种常用语法：

{% raw %}
- **输出变量**：使用双花括号，如 `{{ page.title }}`
- **条件语句**：使用 `{% if %}` ... `{% endif %}`
- **循环语句**：使用 `{% for %}` ... `{% endfor %}`
- **模板继承**：通过 `layout` 在 Front Matter 中指定
{% endraw %}

## 代码示例

下面是一个使用 Jekyll 创建博客列表的示例代码：

{% raw %}
```html
{% for post in site.posts %}
<article>
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p>{{ post.date | date: "%Y-%m-%d" }}</p>
  <p>{{ post.excerpt }}</p>
</article>
{% endfor %}
```
{% endraw %}

## 表格示例

| 功能 | 描述 | 状态 |
|------|------|------|
| Markdown 支持 | 支持 GitHub Flavored Markdown | ✅ |
| Liquid 模板 | 强大的模板引擎 | ✅ |
| 代码高亮 | 使用 Rouge 高亮代码 | ✅ |
| 数学公式 | 支持 LaTeX 语法 | ✅ |

## 数学公式示例

Jekyll 支持数学公式渲染。以下是一些常用公式示例：

### 行内公式

欧拉公式：$e^{i\pi} + 1 = 0$

### 块级公式

二次方程求根公式：

$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

矩阵示例：

$$\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}$$

## 引用样式

> 静态网站生成器的优势在于：不需要数据库，部署简单，加载速度快，安全性高。

## 键盘快捷键提示

使用 <kbd>Ctrl</kbd> + <kbd>S</kbd> 可以快速保存文件，使用 <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> 可以打开命令面板。

## 总结

通过本教程，我们学习了：

1. **Front Matter** 的作用和用法
2. **Liquid 模板** 的基本语法
3. **代码高亮** 的实现方式
4. **数学公式** 的渲染方法
5. **表格、图片、引用** 等内容的展示

Jekyll 是一个非常适合构建个人博客和技术文档的工具，配合 GitHub Pages 可以实现免费的静态网站托管。