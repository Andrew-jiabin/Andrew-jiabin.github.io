# Publishing and Troubleshooting

用途：说明 GitHub Pages 发布注意事项、发布前检查步骤，以及常见问题如何排查。

## GitHub Pages 发布方式

这个仓库是用户站点仓库：

```text
Andrew-jiabin.github.io
```

对应线上地址通常是：

```text
https://Andrew-jiabin.github.io
```

`_config.yml` 中的关键配置：

```yml
url: "https://Andrew-jiabin.github.io"
baseurl: ""
permalink: /blog/:year/:month/:day/:title/
exclude:
  - editing-guide/
```

含义：

- `url` 是网站线上域名。
- `baseurl` 对用户站点应保持为空字符串。
- `permalink` 控制博客默认链接格式。
- `editing-guide/` 不会发布到线上网站。

## 发布前检查清单

提交到 GitHub 前建议检查：

- 首页能打开。
- About、Research、Projects、Publications、Blog、CV、Contact 都能打开。
- 新增博客在 Blog 页面出现。
- 新增项目在 Projects 页面出现。
- 新增论文在 Publications 页面出现。
- CV 下载按钮只在 `cv_pdf` 非空时出现。
- 头像、首页图、博客图、PDF 链接路径正确。
- 中文没有乱码。
- 没有误改 `_layouts/`、`_includes/`、`css/`、`assets/js/`。

## 本地预览

如果本机已经安装 Ruby 和 Jekyll，可以在仓库根目录尝试：

```powershell
jekyll serve
```

如果未来添加了 `Gemfile`，再改用：

```powershell
bundle exec jekyll serve
```

Windows 上第一次安装时，推荐使用 RubyInstaller 的 Ruby+Devkit x64，然后安装 Jekyll 和 Windows 时区依赖：

```powershell
gem install jekyll bundler tzinfo tzinfo-data
```

如果看到 `cannot load such file -- tzinfo`，就是缺少 `tzinfo` 或 `tzinfo-data`。

然后打开本地预览地址，通常是：

```text
http://127.0.0.1:4000
```

注意：

- 当前仓库没有必须依赖 npm 的构建流程。
- 如果本地没有 Ruby/Jekyll，也可以直接提交到 GitHub 后看 Pages 构建结果。
- 本地预览失败不一定代表 GitHub Pages 失败，但 YAML 错误通常两边都会失败。

## GitHub Pages 设置注意

在 GitHub 仓库中检查：

- Repository name 应为 `Andrew-jiabin.github.io`。
- Pages source 应指向主分支，例如 `main` 或 `master`。
- 如果使用 GitHub Actions，要查看 Actions 页面的构建日志。
- 如果使用默认 Pages 构建，要查看 Settings -> Pages 的部署状态。

用户站点不要随意设置 `baseurl`。如果把 `baseurl` 改成 `"/something"`，图片、样式和站内链接可能全部错位。

## 常见问题

### 页面突然无法构建

最常见原因是 YAML 格式错误。

检查：

- 缩进是否仍然是 2 个空格。
- 列表项是否漏了 `-`。
- 文本里有冒号但没有加引号。
- 字符串引号是否成对。
- 是否混用了 tab。

错误示例：

```yml
summary: This text has: a colon
```

推荐写法：

```yml
summary: "This text has: a colon"
```

### 博客没有出现在 Blog 页面

检查：

- 文件是否放在 `_posts/`。
- 文件名是否符合 `YYYY-MM-DD-title.md`。
- 文件开头是否有完整 front matter。
- `date` 是否是未来日期。
- front matter 结束处是否有第二个 `---`。
- 文件扩展名是否是 `.md`。

### 博客链接不符合预期

如果没有写 `permalink`，Jekyll 会根据 `_config.yml` 的 `permalink` 和文章标题生成链接。中文标题或包含空格的标题可能生成不理想的 URL。

推荐每篇博客手写稳定链接：

```yml
permalink: /blog/2026/02/01/agent-workflow-notes/
```

### 中文显示乱码

检查：

- Markdown 和 YAML 文件是否保存为 UTF-8。
- 不要用会把 UTF-8 当作 ANSI 或 GBK 重写的编辑器。
- 在 Windows 上编辑中文时，优先使用能明确保存为 UTF-8 的编辑器。

如果已经乱码，不要继续在乱码基础上大改。应找原始文本或历史版本恢复。

### 图片本地能看到，线上看不到

常见原因：

- 文件名大小写不一致。
- 路径写错。
- 图片没有提交到 GitHub。
- 路径用了反斜杠 `\`，网页中应使用 `/`。

推荐写法：

```md
![Caption](/assets/images/posts/topic/figure.png)
```

不要写：

```md
![Caption](assets\images\posts\topic\figure.png)
```

### PDF 或下载文件打不开

检查：

- 文件是否放在 `assets/files/` 或其子目录。
- 链接是否以 `/assets/files/...` 开头。
- 文件名大小写是否一致。
- PDF 是否真的提交到了 GitHub。

### Publications 页面仍显示 Coming soon

原因：`_data/publications.yml` 的 `items` 仍为空。

把：

```yml
items: []
```

改成：

```yml
items:
  - year: "2026"
    title: "Example title"
    authors:
      - "Jiabin Lin"
    venue: "Preprint"
```

### CV 页面没有下载按钮

原因：`_data/cv.yml` 中 `cv_pdf` 是空字符串。

设置为：

```yml
cv_pdf: "/assets/files/jiabin-lin-cv.pdf"
```

同时确认该 PDF 文件存在。

### Contact 页面没有邮箱或社交链接

这是正常设计。`_data/profile.yml` 中邮箱或社交链接为空时，页面会自动隐藏。

例如：

```yml
email: ""
```

会隐藏邮箱。

### 导航高亮不对

页头根据当前页面 URL 判断哪个导航项激活。如果两个导航项路径互相包含，可能出现高亮异常。

建议：

- 保持导航路径简洁。
- 不要添加重复路径。
- 页面路径以 `/page-name/` 形式书写。

### 样式或代码高亮加载慢

页面使用 jsDelivr 加载 Prism 代码高亮资源。如果网络无法访问 CDN，代码高亮和复制按钮可能不完整，但正文仍应可读。

不要因为 CDN 短暂失败就重写站点结构。只有在长期不可用或明确要离线化时，才考虑把依赖改成本地资源。

### 修改了 `editing-guide/` 但线上没变化

这是正常设计。`editing-guide/` 已经被 `_config.yml` 排除，不会发布到线上网站。

维护文档只服务维护者，不作为网站公开内容。

## 较弱 AI 的排错顺序

如果不知道问题在哪里，按这个顺序检查：

1. 最近改了哪些文件。
2. 如果改了 `_data/*.yml`，先查 YAML 缩进和引号。
3. 如果改了 `_posts/*.md`，先查 front matter。
4. 如果是图片或 PDF 问题，查文件是否存在、路径是否大小写一致。
5. 如果是线上问题但本地没问题，查 GitHub Pages 构建日志和大小写路径。
6. 不要先改 CSS、JS、layout 来掩盖内容数据问题。
