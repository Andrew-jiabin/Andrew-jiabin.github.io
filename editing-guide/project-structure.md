# Project Structure

用途：说明本 Jekyll/GitHub Pages 个人网站的目录结构、页面来源和数据流。适合在改内容前快速判断应该编辑哪个文件。

## 顶层结构

```text
Andrew-jiabin.github.io/
  _config.yml
  index.html
  about.html
  research.html
  projects.html
  publications.html
  blog.html
  cv.html
  contact.html
  _data/
  _posts/
  _layouts/
  _includes/
  assets/
  css/
  editing-guide/
```

## 每个目录的作用

- `_data/`：网站的结构化内容。日常维护最常改这里。
- `_posts/`：博客文章，每篇文章是一个 Markdown 文件。
- `assets/images/`：图片资源，例如头像、首页背景、博客配图、项目配图。
- `assets/files/`：下载文件，例如 CV PDF、论文 PDF、海报、补充材料、演示文稿。
- `assets/js/`：网站交互脚本，目前负责移动端菜单和滚动显示效果。
- `css/`：网站样式。
- `_layouts/`：Jekyll 页面框架，例如普通页面和博客页面的外壳。
- `_includes/`：复用组件，例如页头和页脚。
- `editing-guide/`：维护文档，只给维护者看，不发布到网站。

## 页面和数据来源

| 页面 | 文件 | 主要数据来源 | 维护方式 |
|---|---|---|---|
| Home | `index.html` | `_data/profile.yml`、`_data/home.yml`、`_posts/` 最新文章 | 改首页文字和按钮时优先改数据文件 |
| About | `about.html` | `_data/profile.yml`、`_data/cv.yml` | 改个人简介、focus、经历时改数据文件 |
| Research | `research.html` | `_data/research.yml` | 新增或修改研究方向 |
| Projects | `projects.html` | `_data/projects.yml` | 新增或修改项目条目 |
| Publications | `publications.html` | `_data/publications.yml` | 新增论文、预印本、海报、数据集 |
| Blog | `blog.html` | `_posts/*.md` | 新增或修改博客文章 |
| CV | `cv.html` | `_data/cv.yml` | 改教育、经历、技能、CV PDF |
| Contact | `contact.html` | `_data/profile.yml` | 改邮箱、社交链接、地点、研究关注点 |

## 数据如何进入页面

Jekyll 会把 `_data/profile.yml` 变成 `site.data.profile`，把 `_data/projects.yml` 变成 `site.data.projects`。页面文件里使用 Liquid 语法读取这些数据。

例如，`projects.html` 会循环读取：

```liquid
{% for project in site.data.projects.items %}
```

所以新增项目时，不要复制页面 HTML。只需要在 `_data/projects.yml` 的 `items:` 下新增一项。

## 内容层和功能层的边界

日常内容维护：

- 改 `_data/*.yml`
- 改 `_posts/*.md`
- 添加 `assets/images/` 或 `assets/files/` 里的资源

改版或功能开发：

- 改 `_layouts/`
- 改 `_includes/`
- 改 `css/style.css`
- 改 `assets/js/main.js`
- 改顶层页面 HTML
- 改 `_config.yml`

如果只是增加一条经历、一篇文章、一篇论文或一个项目，通常不需要碰功能层。
