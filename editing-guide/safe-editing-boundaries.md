# Safe Editing Boundaries

用途：明确哪些文件可以日常修改，哪些文件不要轻易改，并给未来 AI 维护者一套保守操作规则。

## 可以日常修改的文件

这些文件是内容源，通常可以根据维护任务直接改：

- `_data/profile.yml`
- `_data/home.yml`
- `_data/navigation.yml`
- `_data/research.yml`
- `_data/projects.yml`
- `_data/publications.yml`
- `_data/cv.yml`
- `_posts/*.md`

这些目录可以添加资源：

- `assets/images/profile/`
- `assets/images/site/`
- `assets/images/posts/`
- `assets/images/projects/`
- `assets/images/research/`
- `assets/files/`

## 谨慎修改的文件

这些文件不是普通内容源。只有在明确改版、修复布局或修复功能时才改：

- `index.html`
- `about.html`
- `research.html`
- `projects.html`
- `publications.html`
- `blog.html`
- `cv.html`
- `contact.html`

原因：

- 它们包含页面结构和 Liquid 循环。
- 日常新增内容不需要改这些文件。
- 错改这些文件可能导致数据不再显示。

## 不要轻易修改的文件和目录

除非用户明确要求改样式、布局、导航组件、脚本行为或构建配置，否则不要改：

- `_layouts/`
- `_includes/`
- `css/style.css`
- `assets/js/main.js`
- `_config.yml`

尤其不要随手修改：

- `_config.yml` 的 `baseurl`
- `_config.yml` 的 `permalink`
- `_config.yml` 的 `exclude`
- `_layouts/post.html`
- `_includes/header.html`
- `css/style.css` 中的响应式规则

## 不要轻易做的事

- 不要删除旧博客文章。
- 不要改旧博客的 `permalink`，除非接受旧链接失效。
- 不要重命名已被引用的图片或 PDF。
- 不要把内容直接写死进页面 HTML，优先写进 `_data`。
- 不要为了隐藏某个空字段而删除页面模板逻辑。
- 不要把维护文档从 `_config.yml` 的 `exclude` 中移除。
- 不要把站点改成需要 npm 构建，除非用户明确要求。
- 不要在没有备份原文的情况下修复乱码文章。

## 给较弱 AI 的操作协议

收到维护任务后，先判断任务类型：

- 个人信息、邮箱、头像、首页按钮：改 `_data/profile.yml`。
- 首页指标和首页介绍卡片：改 `_data/home.yml`。
- 导航栏：改 `_data/navigation.yml`，并确认目标页面存在。
- 研究方向：改 `_data/research.yml`。
- 项目：改 `_data/projects.yml`。
- 论文或学术输出：改 `_data/publications.yml`。
- 教育、经历、技能、CV PDF：改 `_data/cv.yml`。
- 博客文章：改或新增 `_posts/*.md`。
- 图片：放到 `assets/images/` 的合适子目录。
- PDF 或附件：放到 `assets/files/`。

执行时遵守：

1. 先读相关现有文件，模仿已有结构。
2. 只改任务需要的文件。
3. 保持 YAML 缩进和字段名一致。
4. 不发明页面模板没有使用的新字段，除非只是为未来保留且不会破坏构建。
5. 中文内容保存为 UTF-8。
6. 新增链接后检查路径。
7. 完成后报告文件清单和每个文件用途。

## 判断是否需要改功能层

只有出现以下需求时，才考虑功能层：

- 页面需要新布局，例如 Publications 要分组显示。
- Projects 要显示项目图片，而当前模板没有图片字段。
- 需要新增一个全新页面。
- 需要修改移动端菜单行为。
- 需要改全站视觉风格。
- GitHub Pages 构建配置需要调整。

如果任务只是“新增一篇博客”“新增一个项目”“更新 CV”“更新邮箱”，不需要改功能层。

## 修改前后检查表

修改前：

- 确认用户要求的范围。
- 确认要改的是内容层还是功能层。
- 找到相关 `_data` 或 `_posts` 文件。

修改中：

- 保持字段顺序尽量接近已有条目。
- 保持列表缩进一致。
- 对包含特殊字符的文本加双引号。
- 内部链接用 `/path/`，资源链接用 `/assets/...`。

修改后：

- 检查是否只改了必要文件。
- 检查新增 YAML 是否能被 Jekyll 解析。
- 检查新增 Markdown 是否有 front matter。
- 检查图片和文件是否位于正确目录。
- 报告改动文件清单。

## 什么时候应停下来问用户

遇到这些情况不要猜：

- 用户要求新增一个页面，但没有说明页面名称或导航位置。
- 用户提供论文但没有说明是否已经公开。
- 用户提供 CV PDF 但没有说明是否替换旧版。
- 用户要求改邮箱或社交链接，但没有给具体地址。
- 用户要求删除内容，但没有说明是否保留历史。
- 用户要求大幅改版，但同时说不要改功能文件。

如果只是字段内容缺失，可以先保留空字符串或省略链接，不要编造信息。
