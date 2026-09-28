# CLAUDE.md

张晨宇的个人学术主页,基于 Academic Pages Jekyll 模板,推送到 `master` 后由
GitHub Pages 自动部署到 <https://chenyuzhangx.github.io>。

## 本地预览

```bash
./local/preview-env/serve.sh   # http://localhost:4000,改动自动重建+浏览器刷新
```

- **不要**用仓库根目录的 `Gemfile` 跑本地预览:它锁定 GitHub Pages 的老版
  Jekyll 3.9,在新版 Ruby(3.4+)上缺 `csv` 等库跑不起来;系统自带 Ruby 2.6
  也太旧。预览环境独立放在 `local/preview-env/`(Jekyll 4 + Homebrew Ruby),
  详见 `local/preview-env/README.md`。
- `local/` 已被 `.gitignore` 和 `_config.yml` 排除,不进 git、不参与构建。
- 改 `_config.yml` 后需重启 serve.sh;改 Markdown/HTML/SCSS 会自动生效。

## 站点结构

单页设计:首页即全部内容,导航栏只有 Publications / CV 两个锚点链接。

| 位置 | 作用 |
|---|---|
| `_pages/about.md` | 首页正文(About Me),末尾 include 下面两个区块 |
| `_includes/section-publications.html` | 首页论文列表(按年份分组,日期倒序) |
| `_includes/section-cv.html` | 首页 Education / Honors 时间线(纯手写 HTML) |
| `_publications/*.md` | 每篇论文一个文件,内容全在 front matter 里 |
| `CATok/` | CATok 项目展示页(独立 HTML/CSS,不经 Jekyll 模板) |
| `_config.yml` | 作者信息、侧边栏社交链接等站点级配置 |

以下目录是**模板残留的示例内容,未在站点上使用**,除非明确要启用对应功能,
否则不要改:`_posts/`、`_talks/`、`_teaching/`、`_portfolio/`、`_drafts/`、
`_data/cv.json`、`markdown_generator/`、`talkmap*`。`backup/` 是旧版备份,
已被 `_config.yml` 排除。

## 论文条目约定

`_publications/` 下文件的 front matter 字段:

```yaml
title: "..."
category: accepted          # submissions(在投)/ accepted(已录用)/ conferences 等(已发表)
venue: '...'                # 会议期刊名;submissions 且为空时只显示 "In Submission"
date: 2026-06-01            # 决定年份分组和排序
website: /CATok/            # 可选,渲染 "Project Page" 链接
bibtexurl: /files/xxx.bib   # 可选,渲染 "BibTeX" 链接
teaser: [/images/publications/xxx.png]
authors:                    # name 必填;url / co_first / corresponding 可选
  - name: 'Chenyu Zhang'
    co_first: true
```

- `category` 决定状态文案:"In Submission to" / "Accepted to" / "Published in",
  渲染逻辑共四处,改动需同步:`_includes/section-publications.html`、
  `_layouts/single.html`、`_includes/archive-single.html`、
  `_includes/archive-single-cv.html`。
- venue 用全称加缩写,如 `Conference on Neural Information Processing Systems (NeurIPS)`。
- 录用但未正式发表用 `accepted`,正式发表后改成 `conferences` 等类别。
- 作者中与本站主同名的自动加粗,无需手动标记。

## 工作约定

- 改动页面可见内容后,先用本地预览验证渲染效果再提交。
- 提交只 add 相关文件;`_publications/source/` 是有意不跟踪的目录。
