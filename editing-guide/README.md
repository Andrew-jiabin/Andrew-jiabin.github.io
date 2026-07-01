# Personal Website Editing Guide

用途：这是维护本 Jekyll/GitHub Pages 个人网站的入口说明。未来用户和 AI 维护者应先读本文件，再按任务跳到对应文档。

## 先看这几条

1. 日常维护优先改 `_data/*.yml` 和 `_posts/*.md`。
2. 图片、PDF、简历、论文附件等静态资源放在 `assets/` 下。
3. 不要为了改一段文字去修改 `_layouts/`、`_includes/`、`css/style.css` 或 `assets/js/main.js`。
4. `editing-guide/` 已在 `_config.yml` 的 `exclude` 中排除，不会发布到线上网站。
5. 所有中文文件都应保存为 UTF-8，尤其是 `_posts/*.md`。

## 文档清单

- `README.md`：入口索引，说明应该先读什么。
- `project-structure.md`：解释项目结构、页面和数据文件之间的关系。
- `content-editing-guide.md`：详细说明每个 `_data` 文件怎么改、怎么新增博客、项目、论文、CV 项，以及图片和文件放哪里。
- `visual-style.md`：说明当前鲜活多色视觉方向，以及如何避免改回课题组网站同色系。
- `publishing-and-troubleshooting.md`：说明 GitHub Pages 发布注意事项、检查步骤和常见问题排查。
- `safe-editing-boundaries.md`：列出哪些文件可以日常改，哪些文件不要轻易改，并给较弱 AI 的操作规则。

## 推荐维护流程

1. 判断任务类型：
   - 改个人信息、研究方向、项目、论文、CV：看 `content-editing-guide.md`。
   - 新增博客：看 `content-editing-guide.md` 的博客章节。
   - 发布失败、图片不显示、博客不出现：看 `publishing-and-troubleshooting.md`。
   - 不确定能不能改某个文件：看 `safe-editing-boundaries.md`。
2. 修改前先查看相关页面使用了哪些数据文件。
3. 修改后至少检查 YAML 缩进、链接路径、图片路径和中文编码。
4. 提交前报告改了哪些文件，以及改动用途。

## 这个站点的维护原则

本网站是数据驱动的个人站。页面结构已经写好，内容主要从 `_data/*.yml` 和 `_posts/*.md` 读入。

这意味着：

- 改一句个人简介，不应重写 `about.html`。
- 新增一个项目，不应复制一整张项目卡片 HTML，而应在 `_data/projects.yml` 里新增一个 `items` 条目。
- 新增一篇博客，应放入 `_posts/`，并写好 front matter。
- 上传 CV PDF，应放入 `assets/files/`，再在 `_data/cv.yml` 中填写 `cv_pdf` 路径。

如果你是 AI 维护者，除非用户明确要求改版或修复功能，否则请只做内容层修改。
