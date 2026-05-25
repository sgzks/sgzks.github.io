---
layout: post
title: "实验过程中遇到的问题及解决方案"
date: 2026-05-26
category: "实验记录"
tags: ["Jekyll", "GitHub Pages", "LaTeX", "问题解决"]
author: "第七组：张静火、王翼龙、厉传禹、张祎涵、王子潭"
---

在本次创新实验网站搭建与部署过程中，我们遇到了一些格式、构建和本地调试方面的问题。下面记录三个较有代表性的问题及对应解决方案。

## 问题一：LaTeX 公式格式显示不正确

**问题现象：**  
在编写数学相关内容时，部分 LaTeX 公式没有正常渲染，而是直接显示为原始文本。例如行内公式和块级公式混用时，页面中会出现 `$`、`\frac`、`\sqrt` 等源码内容。

**原因分析：**  
主要原因是公式分隔符使用不规范，或者块级公式前后缺少独立空行。行内公式应使用 `$...$`，块级公式应使用 `$$...$$`。如果公式中括号、上下标或转义符写错，也会导致 KaTeX 无法解析。

**解决方案：**  
统一使用规范的 LaTeX 写法。行内公式写成 `$E=mc^2$`，块级公式单独成段，例如：

$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

同时检查页面模板中是否引入了 KaTeX 渲染脚本，确保 Markdown 生成 HTML 后公式能够被自动渲染。

## 问题二：上传到 GitHub 后 Pages 构建失败

**问题现象：**  
网站推送到 GitHub 后，Actions 构建失败，日志中出现：

```text
The process '/opt/hostedtoolcache/Ruby/3.1.7/x64/bin/bundle' failed with exit code 5
```

同时还出现了 `actions/configure-pages@v5` 使用 Node.js 20 的弃用警告。

**原因分析：**  
本地项目的 `Gemfile.lock` 是使用 Ruby 4.0.5 和 Bundler 4.0.12 生成的，但 GitHub Actions 工作流中配置的是 Ruby 3.1。两边 Ruby/Bundler 环境不一致，导致 `bundle install` 或 `bundle exec` 阶段失败。

**解决方案：**  
修改 `.github/workflows/pages.yml`，将 Ruby 版本与本地锁文件保持一致，并升级 Pages 相关 actions：

```yaml
- name: Setup Pages
  uses: actions/configure-pages@v6

- name: Setup Ruby
  uses: ruby/setup-ruby@v1
  with:
    ruby-version: '4.0'
    bundler-cache: true

- name: Upload artifact
  uses: actions/upload-pages-artifact@v5
```

修改后重新提交并推送，GitHub Pages 可以使用一致的环境完成构建。

## 问题三：本地预览端口被占用

**问题现象：**  
本地想通过 Jekyll 预览网站时，默认的 `4000` 端口已经被其他程序占用；尝试使用 `4001` 时，也发现该端口被 QQ 进程占用，导致 Jekyll 无法启动服务。

**原因分析：**  
Jekyll 本地服务需要绑定一个可用端口。如果端口已经被系统中的其他应用监听，启动时就会出现绑定失败或页面无法访问的问题。

**解决方案：**  
先使用端口检查命令确认端口占用情况，再换用未被占用的端口启动服务。本次最终使用 `4100` 端口：

```powershell
bundle exec jekyll serve --host 127.0.0.1 --port 4100 --livereload
```

启动成功后，在浏览器访问 `http://127.0.0.1:4100/`，即可查看本地预览效果。

## 总结

通过这些问题的排查，我们进一步熟悉了 Jekyll 网站的内容编写规范、GitHub Pages 自动部署流程，以及本地开发调试方法。遇到问题时，先观察报错信息，再定位配置、依赖和运行环境，通常可以更快找到解决方案。
