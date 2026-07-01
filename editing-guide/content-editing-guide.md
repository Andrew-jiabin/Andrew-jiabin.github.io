# Content Editing Guide

用途：详细说明每个 `_data` 文件怎么改，如何新增博客、项目、论文和 CV 项，以及图片和文件应该放在哪里。

## 通用 YAML 规则

`_data/*.yml` 使用 YAML。请遵守这些规则：

- 缩进用 2 个空格，不要用 tab。
- 列表项以 `-` 开头，同一级列表缩进必须一致。
- 文本建议加双引号，尤其是包含冒号、斜杠、中文标点或特殊符号时。
- 暂时没有内容时，用空字符串 `""` 或空列表 `[]`。
- 内部链接建议从网站根路径开始，例如 `"/projects/"`、`"/assets/files/cv.pdf"`。
- 外部链接写完整 URL，例如 `"https://github.com/Andrew-jiabin"`。
- 修改后如果页面突然打不开，优先检查 YAML 缩进和引号。

## `_data/profile.yml`

用途：控制全站个人基础信息、头像、联系方式、社交链接和首页按钮。

主要影响页面：

- Home
- About
- Contact
- 页头品牌区
- 页脚

字段说明：

- `name`：正式姓名，常用于图片 alt 和资料展示。
- `display_name`：页面主标题显示的名字。
- `short_name`：页头左上角显示的短名。
- `role`：身份，例如 `Graduate student`。
- `affiliation`：机构，例如 `Peking University`。
- `location`：地点。
- `email`：邮箱。留空 `""` 时 Contact 和页脚不会显示邮箱。
- `avatar`：头像路径，当前放在 `assets/images/profile/`。
- `tagline`：短句，主要用于首页和页脚。
- `intro`：较长个人简介，Home 和 About 会显示。
- `focus`：关注方向列表，Home、About、Contact 都会用到。
- `social`：社交链接。某个平台的 `url` 留空时不会显示。
- `hero_actions`：首页主按钮。`style` 目前建议只用 `primary` 或 `secondary`。

修改邮箱示例：

```yml
email: "your.name@example.com"
```

新增或启用社交链接示例：

```yml
social:
  github:
    label: "GitHub"
    url: "https://github.com/Andrew-jiabin"
  scholar:
    label: "Google Scholar"
    url: "https://scholar.google.com/..."
```

更换头像：

1. 把新头像放到 `assets/images/profile/`，例如 `assets/images/profile/jiabin-lin-2026.png`。
2. 修改：

```yml
avatar: "/assets/images/profile/jiabin-lin-2026.png"
```

注意：路径大小写要和文件名完全一致。GitHub Pages 对大小写更严格。

## `_data/home.yml`

用途：控制首页的快速入口和首页下方的几个介绍入口。

主要影响页面：

- Home

字段说明：

- `metrics`：首页第一组快速入口。每项包含：
  - `value`：醒目的短词或数字。
  - `label`：说明文字。
  - `url`：点击后跳转的页面。
- `featured_sections`：首页介绍区。每项包含：
  - `eyebrow`：小标签。
  - `title`：标题。
  - `text`：说明文字。
  - `url`：点击后跳转的页面。

建议：

- `metrics` 建议保持 2 到 4 项，太多会显得拥挤。
- `featured_sections` 建议保持 2 到 4 项。它们会显示为轻量列表，不是大卡片。
- `url` 应该指向已有页面，例如 `"/research/"`、`"/projects/"`、`"/blog/"`。

## `_data/navigation.yml`

用途：控制页头导航栏。

主要影响页面：

- 全站页头

每项包含：

- `label`：导航显示文字。
- `url`：导航目标路径。

示例：

```yml
- label: "Projects"
  url: "/projects/"
```

注意：

- 不要添加不存在的页面链接。
- 如果新增导航项，通常还需要新增对应页面文件或确认目标页面已存在。
- Home 的路径应保持为 `"/"`。
- 其他页面路径建议以 `/` 开头和结尾，例如 `"/research/"`。

## `_data/research.yml`

用途：控制 Research 页面上的研究方向。

主要影响页面：

- Research

字段说明：

- `intro`：Research 页顶部说明。
- `areas`：研究方向列表。每项包含：
  - `title`：方向标题。
  - `anchor`：页面内锚点 ID，用于链接到具体方向。
  - `summary`：短摘要。
  - `details`：要点列表。
  - `keywords`：关键词标签。

新增研究方向示例：

```yml
areas:
  - title: "AI agents for scientific workflows"
    anchor: "ai-agents"
    summary: "Designing agent systems that can plan, use tools, inspect evidence, and leave readable traces."
    details:
      - "Workflow decomposition and verification loops."
      - "Tool use around data, code, and browser tasks."
    keywords:
      - "Agents"
      - "Tool use"
      - "Verification"
```

`anchor` 建议：

- 用英文小写。
- 单词之间用短横线。
- 不要有空格、中文、斜杠或特殊符号。
- 每个 `anchor` 必须唯一。

## `_data/projects.yml`

用途：控制 Projects 页面上的项目条目。

主要影响页面：

- Projects

字段说明：

- `intro`：Projects 页顶部说明。
- `items`：项目列表。每项包含：
  - `title`：项目名。
  - `slug`：项目条目的 HTML ID，必须唯一。
  - `status`：状态，例如 `Exploration`、`Active notes`、`Maintained`、`Paused`。
  - `summary`：项目简介。
  - `role`：你的角色。
  - `year`：年份。
  - `keywords`：关键词列表，会显示为一行轻量文字。
  - `links`：相关链接列表。每个链接包含 `label` 和 `url`。

新增项目示例：

```yml
items:
  - title: "New Research Tool"
    slug: "new-research-tool"
    status: "Exploration"
    summary: "A short description of what the tool does and why it matters."
    role: "Designer and builder"
    year: "2026"
    keywords:
      - "AI"
      - "Research workflow"
      - "Prototype"
    links:
      - label: "GitHub"
        url: "https://github.com/Andrew-jiabin/example"
      - label: "Related note"
        url: "/blog/2026/01/12/hello-agents-task-00/"
```

项目维护建议：

- `slug` 用英文小写和短横线，例如 `personal-website-system`。
- `summary` 不要太长，项目条目里 1 到 2 句最合适。
- `links` 可以省略，但如果保留，必须是列表。
- 内部链接用站内路径，外部链接用完整 `https://...`。

## `_data/publications.yml`

用途：控制 Publications 页面上的论文、预印本、海报、数据集或 workshop abstract。

主要影响页面：

- Publications

当前文件为空列表：

```yml
items: []
```

当 `items` 为空时，页面显示 `empty_state`。一旦新增条目，页面会显示 publication list。

建议字段：

- `year`：年份。
- `title`：题名。
- `authors`：作者列表。
- `venue`：期刊、会议、预印本平台、课程项目或海报场景。
- `status`：可选状态，例如 `In preparation`、`Preprint`、`Accepted`、`Published`。
- `links`：可选链接列表。

新增论文示例：

```yml
items:
  - year: "2026"
    title: "Title of the paper or preprint"
    authors:
      - "Jiabin Lin"
      - "Collaborator Name"
    venue: "Preprint"
    status: "In preparation"
    links:
      - label: "PDF"
        url: "/assets/files/papers/example-paper.pdf"
      - label: "Code"
        url: "https://github.com/Andrew-jiabin/example"
```

注意：

- `authors` 必须是列表，因为页面会用逗号把作者合并显示。
- 如果论文 PDF 还没公开，不要放空链接项，直接先省略 `links`。
- 如果放论文 PDF，建议路径为 `assets/files/papers/文件名.pdf`。

## `_data/cv.yml`

用途：控制 About 时间线和 CV 页面。

主要影响页面：

- About
- CV

字段说明：

- `education`：教育经历列表。每项包含：
  - `degree`
  - `institution`
  - `period`
  - `details`
- `experience`：经历列表。每项包含：
  - `title`
  - `organization`
  - `period`
  - `details`
- `skills`：技能组。每组包含：
  - `group`
  - `items`
- `awards`：目前页面未显示，但可保留给未来扩展。
- `cv_pdf`：CV PDF 路径。留空时不会显示下载按钮。

新增教育经历示例：

```yml
education:
  - degree: "Graduate student"
    institution: "Peking University"
    period: "2026-present"
    details:
      - "Research interests include AI tools for scientific workflows, optical sensing, and biomedical imaging."
```

新增经历示例：

```yml
experience:
  - title: "Research Assistant"
    organization: "Lab or project name"
    period: "2026"
    details:
      - "Built a reproducible analysis workflow."
      - "Prepared notes, figures, and project documentation."
```

新增技能组示例：

```yml
skills:
  - group: "Programming"
    items:
      - "Python"
      - "JavaScript"
      - "Markdown"
```

添加可下载 CV：

1. 把 PDF 放到 `assets/files/`，例如 `assets/files/jiabin-lin-cv.pdf`。
2. 修改：

```yml
cv_pdf: "/assets/files/jiabin-lin-cv.pdf"
```

## 新增博客文章

博客文件放在 `_posts/`。

推荐文件名：

```text
YYYY-MM-DD-short-english-slug.md
```

示例：

```text
2026-02-01-agent-workflow-notes.md
```

虽然中文文件名也可以用，但为了链接和跨平台兼容，推荐文件名使用英文、小写、短横线。

每篇博客开头必须有 front matter：

```md
---
layout: post
title: "Article title"
date: 2026-02-01
category: "Research notes"
permalink: /blog/2026/02/01/agent-workflow-notes/
---

正文从这里开始。
```

字段说明：

- `layout: post`：使用博客文章布局。
- `title`：文章标题，可中文。
- `date`：发布日期，格式建议 `YYYY-MM-DD`。
- `category`：分类标签，可选但推荐。
- `permalink`：固定链接。推荐手写，避免中文标题生成不稳定 URL。

写博客时注意：

- Markdown 正文和 front matter 之间要有第二个 `---`。
- 如果文章日期是未来日期，Jekyll 默认可能不会显示它。
- 中文文章必须保存为 UTF-8。
- 文章中图片路径建议使用站内绝对路径。

博客配图示例：

```md
![Workflow diagram](/assets/images/posts/2026-02-01-agent-workflow/diagram.png)
```

推荐把该图片放在：

```text
assets/images/posts/2026-02-01-agent-workflow/diagram.png
```

## 新增项目

项目不是单独页面，而是 Projects 页面上的条目。新增项目时改 `_data/projects.yml`。

步骤：

1. 在 `items:` 下复制一个已有项目条目的结构。
2. 改 `title`、`slug`、`status`、`summary`、`role`、`year`。
3. 根据需要改 `keywords`。
4. 根据需要添加 `links`。
5. 确认 `slug` 不和其他项目重复。

如果项目有图片，目前 Projects 页面模板不会显示项目图片。可以先把图片放到 `assets/images/projects/项目-slug/`，等未来改版时再接入。

## 新增论文或学术输出

论文、预印本、海报、数据集都放在 `_data/publications.yml` 的 `items:` 中。

步骤：

1. 如果当前是 `items: []`，改成多行列表。
2. 添加 `year`、`title`、`authors`、`venue`。
3. 有状态时添加 `status`。
4. 有公开资源时添加 `links`。
5. PDF、海报、补充材料放到 `assets/files/`。

推荐文件位置：

```text
assets/files/papers/
assets/files/posters/
assets/files/slides/
assets/files/datasets/
```

链接示例：

```yml
links:
  - label: "PDF"
    url: "/assets/files/papers/example-paper.pdf"
  - label: "Poster"
    url: "/assets/files/posters/example-poster.pdf"
```

## 新增 CV 项

教育和经历都在 `_data/cv.yml`。

步骤：

1. 判断是教育、经历还是技能。
2. 在对应列表中新增条目。
3. 保持字段名一致。
4. `details` 每条尽量短，适合页面显示。

时间顺序建议：

- 最新的条目放在最前面。
- `period` 可以写 `2026-present`、`2025-2026` 或 `2026`。

## 图片放哪里

推荐位置：

- 头像：`assets/images/profile/`
- 首页或全站装饰图：`assets/images/site/`
- 博客配图：`assets/images/posts/YYYY-MM-DD-topic/`
- 项目图片：`assets/images/projects/project-slug/`
- 研究图示：`assets/images/research/topic-slug/`

路径写法：

```yml
avatar: "/assets/images/profile/jiabin-lin.png"
```

```md
![Figure caption](/assets/images/posts/2026-02-01-topic/figure.png)
```

图片建议：

- 文件名用英文小写、短横线。
- 避免空格和中文文件名。
- 网站图片优先用 `.png`、`.jpg` 或 `.webp`。
- 大图尽量压缩，避免首页加载太慢。

## 文件放哪里

下载类文件放在 `assets/files/`。

推荐位置：

- CV：`assets/files/jiabin-lin-cv.pdf`
- 论文：`assets/files/papers/`
- 海报：`assets/files/posters/`
- 幻灯片：`assets/files/slides/`
- 补充材料：`assets/files/supplementary/`

链接写法：

```md
[Download CV](/assets/files/jiabin-lin-cv.pdf)
```

```yml
cv_pdf: "/assets/files/jiabin-lin-cv.pdf"
```

## 提交前内容检查

提交前至少检查：

- YAML 缩进是否一致。
- 是否有未闭合的引号。
- 新增链接是否能打开。
- 图片路径大小写是否正确。
- 中文是否仍然正常显示。
- 新增博客是否有完整 front matter。
- 新增博客日期是否不是误写成未来日期。
- 没有为了内容修改而误改布局、样式或脚本。
