# 操作手册：Docsify 安全笔记博客 + GitHub Pages

本文说明从 **零** 到 **可访问站点** 的步骤，以及日常 **增删改查** 与常见问题。技术栈为 **Docsify**（纯前端读取 Markdown）+ **GitHub Pages**（免费、无需自有服务器与备案）。

---

## 一、你将得到什么

| 需求 | 实现方式 |
| --- | --- |
| Markdown 写笔记、网页粘贴 | 编辑 `docs/` 下 `.md` 文件 |
| 代码高亮 + 行号 | `index.html` 引入 Prism + `line-numbers`；正文里正常 Markdown 代码块 |
| 分类（五大块） | 五个子目录 + `docs/_sidebar.md` 分组 |
| 标签 | 每篇文章顶部 `post-meta` 区块（可复制各目录 `_template.md`） |
| 站内搜索 | Docsify `search` 插件 |
| 免费、GitHub Pages | 使用仓库 `/docs` 作为站点根 |
| 项目 / Git 链接 | `docs/projects.md` + 顶部 `docs/_navbar.md` |
| 极简技术风 | `docs/style.css` 可继续改 |
| 后期增删改查 | 对 Git 仓库文件的增删改 + 侧边栏链接维护（见第四节） |

---

## 二、一次性部署步骤

### 1. 准备 GitHub 账号与 Git

- 注册并登录 [GitHub](https://github.com/)。
- 本机安装 [Git](https://git-scm.com/)（Windows 可装 Git for Windows）。

### 2. 把项目放到 GitHub 上

**方式 A：网页新建仓库后上传**

1. GitHub 右上角 **New repository**，仓库名例如 `security-notes-blog`，**Public**，不要勾选自动添加 README（若你本地已有完整文件可忽略）。
2. 在本机进入本项目根目录 `security-notes-blog`（包含 `docs` 与 `README.md` 的那一层）。
3. 在终端执行（把 URL 换成你的仓库地址）：

```bash
git init
git add .
git commit -m "Initial commit: Docsify blog for GitHub Pages"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

**方式 B：GitHub Desktop**

用 [GitHub Desktop](https://desktop.github.com/) 添加本地仓库并 Publish 到 GitHub 即可。

### 3. 开启 GitHub Pages

1. 打开仓库页面 → **Settings** → 左侧 **Pages**。
2. **Build and deployment** → **Source** 选 **Deploy from a branch**。
3. **Branch** 选 `main`（或你的默认分支），**Folder** 选 **`/docs`**，点击 **Save**。
4. 同一页稍等片刻，会显示站点地址，一般为：  
   `https://<用户名>.github.io/<仓库名>/`

> 若仓库名为 `<用户名>.github.io` 且你从 **根目录** 发布站点，则需把 `docs` 里的文件挪到仓库根目录并在 Pages 里选 **/(root)**。本模板默认采用 **`/docs` 文件夹** 发布，与普通仓库名兼容。

### 4. 建议配置：仓库描述与 Topics

在仓库 **About** 里填写站点简介，添加 `docsify`、`github-pages`、`security` 等 Topics，方便招聘方一眼看到。

### 5. 打开 GitHub 角标（可选）

编辑 `docs/index.html`，找到：

```js
repo: "",
```

改为：

```js
repo: "你的用户名/仓库名",
```

保存、提交、推送后刷新站点。

---

## 三、目录说明（维护时只看这里）

```text
security-notes-blog/
├── README.md                 # 仓库说明（简短）
├── MANUAL.md                 # 本操作手册
└── docs/                     # GitHub Pages 根目录
    ├── .nojekyll             # 避免 Jekyll 忽略下划线文件
    ├── index.html            # Docsify 入口与插件配置
    ├── style.css             # 极简主题覆盖
    ├── README.md             # 站点首页内容
    ├── _sidebar.md           # 左侧目录（分类 + 文章链接）
    ├── _navbar.md            # 顶栏链接
    ├── projects.md           # 项目与 Git 链接
    ├── guide/edit-guide.md   # 站内「增删改查」说明
    ├── java-code-audit/      # 分类：Java 代码审计
    ├── src/                  # 分类：SRC
    ├── intranet/             # 分类：内网
    ├── security-knowledge/   # 分类：网安知识
    └── ctf/                  # 分类：CTF
```

各分类目录下均有 **`_template.md`**，新建文章时复制后改名即可。

---

## 四、日常「增删改查」

### 新增（Create）

1. 在对应分类目录新建 `xxx.md`（或复制 `_template.md`）。
2. 用 Markdown 写正文；代码块写法：

````markdown
```java
// 代码
```
````

3. 编辑 `docs/_sidebar.md`，在对应 **分类** 下增加一行链接，例如：  
   `* [我的笔记标题](java-code-audit/my-note.md)`
4. `git add` → `git commit` → `git push`。

### 查询（Read）

- 浏览器打开站点阅读。
- 左上角 **搜索框**：全文搜索标题与正文。
- GitHub 仓库里 **Go to file** 搜索文件名。

### 修改（Update）

直接改对应 `.md` 后推送；**若重命名文件**，需同步改 `_sidebar.md` 里的路径。

### 删除（Delete）

删除 `.md` 文件，并删掉 `_sidebar.md` 中对应条目，再推送。

### 在 GitHub 网页上直接编辑

打开任意 `.md` → 铅笔图标 **Edit** → 粘贴 Markdown → **Commit changes**。同样别忘了更新 `_sidebar.md`（若新增文章）。

---

## 五、分类与标签约定

- **分类**：由 **文件夹** + **`_sidebar.md` 分组标题** 共同体现，对应关系固定为：

  1. `java-code-audit` — Java 代码审计  
  2. `src` — SRC  
  3. `intranet` — 内网  
  4. `security-knowledge` — 网安知识  
  5. `ctf` — CTF  

- **标签**：模板里使用 HTML 一行展示（可搜、可读性好），你可改成纯 Markdown，只要自己能坚持统一格式即可。

---

## 六、代码高亮语言扩展

默认已加载：Java、JavaScript、TypeScript、Bash、PowerShell、Python、YAML、JSON、SQL、HTTP、Markdown 等。

若需要更多语言，在 `docs/index.html` 中 Docsify 主脚本 **之后** 按 Prism 官方组件追加一行，例如 Go：

```html
<script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/components/prism-go.min.js"></script>
```

语言名与 Markdown 围栏一致，例如 ` ```go `。

---

## 七、常见问题

**1. 打开站点空白或一直「加载中」**

- 确认 Pages 使用的是 **`/docs`** 且 `docs/index.html` 已推送。
- 按 `F12` 看 **Console** 是否拦截了 CDN；公司网络可能屏蔽 jsDelivr，可换手机流量测试或改用其他 CDN 镜像（需自行改 `index.html` 里的链接）。

**2. 样式错乱**

- 确认 `docs/style.css` 与 `index.html` 在同一目录且未被改名。

**3. 搜索不到新文章**

- 强刷 `Ctrl+F5`；搜索插件有本地缓存，换浏览器或隔一段时间再试。

**4. 自定义域名**

- 在 `docs/` 下放无后缀文件 `CNAME`，内容一行：你的域名。  
- 在域名 DNS 按 GitHub 文档配置 `CNAME` 或 `A` 记录。  
- Pages 设置里填入 Custom domain。  
（无域名则忽略本条。）

---

## 八、与「数据库型博客」的区别

Docsify **运行时**在浏览器里拉取 Markdown 文件，**没有** PHP/Node 后台，也**没有**传统意义上的数据库 CRUD。你的「库」就是 **Git 仓库**；**增删改查 = 文件 + 侧边栏链接 + Git 推送**。优点是零成本、可版本回滚；缺点是无在线评论系统（可用 GitHub Discussions / Issues 替代，需另做链接）。

---

至此，你已具备一套可长期维护、适合贴在简历上的 **技术向静态笔记站**。若你希望改为 **Hugo / Jekyll / Hexo** 等生成 HTML 的架构，那是另一条路线；当前方案最贴合你提出的 **Docsify + 免服务器** 需求。
