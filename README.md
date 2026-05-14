# 安全笔记博客（Docsify + GitHub Pages）

本仓库为 **免费静态博客**：Markdown 写作、GitHub Pages 托管、站内全文搜索、代码高亮与行号、五大分类 + 标签约定、项目链接页。

- **站点源码目录**：`docs/`（GitHub Pages 指向此目录）
- **操作手册（部署与维护）**：[MANUAL.md](MANUAL.md)

## 快速开始

1. 将本文件夹推送到你的 GitHub 仓库。
2. 仓库 **Settings → Pages**：**Build and deployment** 选择 **Deploy from a branch**，Branch 选默认分支（一般为 `main`），文件夹选 **`/docs`**，保存。
3. 等待 1 分钟左右，访问 `https://<用户名>.github.io/<仓库名>/`。

将 `docs/index.html` 里的 `repo: ""` 改为 `"你的用户名/仓库名"` 可显示 Docsify 自带 GitHub 角标。
