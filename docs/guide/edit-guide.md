# 维护说明：增删改查

Docsify **没有后台数据库**，内容就是仓库里的 Markdown 文件。所谓 **增删改查** 即对仓库文件的 **Git 操作**（本地或 GitHub 网页均可）。

## 新增文章

1. 在对应分类目录下复制该目录下的 `_template.md` 为新文件名，例如 `docs/java-code-audit/my-note.md`（各分类目录均自带 `_template.md`）。
2. 修改标题、标签、正文；代码块使用三个反引号并写上语言，例如 ` ```java `。
3. 打开 `docs/_sidebar.md`，在对应分类下增加一行：  
   `* [显示标题](java-code-audit/my-note.md)`
4. `git add` → `git commit` → `git push`。GitHub Pages 约 **1 分钟内** 生效。

## 修改文章

直接编辑对应 `.md` 文件并推送。无需改侧边栏（除非改文件名或路径）。

## 删除文章

1. 删除对应 `.md` 文件（或网页端 Delete）。
2. 从 `docs/_sidebar.md` 中删除指向该文的链接。
3. 提交并推送。

## 查询 / 检索

- **站内**：使用站点左上角 **搜索框**（全文）。
- **仓库内**：GitHub 仓库页 `Go to file` 或 `t` 快捷键搜索文件名。

## 分类与标签约定

- **分类**：由 **目录 + 侧边栏分组** 表示，五大块对应 `java-code-audit`、`src`、`intranet`、`security-knowledge`、`ctf`。
- **标签**：每文顶部一行 `**标签**：`，便于自己扫读；搜索插件会索引正文，标签关键字可被搜到。

## 在 GitHub 上直接粘贴写作

1. 进入仓库 `docs/` 下目标目录。
2. **Add file → Create new file**，粘贴 Markdown。
3. 到 `_sidebar.md` 增加链接后 **Commit**。

或使用 **`.`** 键 / `github.dev` 打开网页版 VS Code 编辑整个 `docs` 目录。

## 常见问题

**Q：代码没有行号？**  
确认 `index.html` 已加载 `prism-line-numbers`；代码块外层 `pre` 在渲染后会带 `line-numbers` 类（由内置插件添加）。若与某浏览器插件冲突，可无痕模式试一次。

**Q：搜索不到新文章？**  
清浏览器缓存或硬刷新；搜索有 `maxAge` 缓存，隔日或换浏览器再试。

**Q：页面 404？**  
检查 GitHub Pages 是否选择 **`/docs` 文件夹** 作为来源，且默认分支包含 `docs/index.html`。
