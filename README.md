# 个人主页

纯手写 HTML / CSS 的静态个人主页。**零依赖、零构建、零外部请求**（不加载 Google Fonts / CDN，国内打开也不会卡在字体上）。

```
index.html     页面结构（改文字、链接都在这里）
style.css      样式（配色集中在文件顶部的 :root 变量里）
favicon.svg    站点图标
_headers       Cloudflare Pages 的响应头配置（自动生效，不用管）
```

## 本地预览

```bash
cd website
python3 -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 要改的地方

| 想改什么 | 改哪里 |
|---|---|
| 名字、自我介绍、链接 | `index.html`（搜 `你的名字`、`yourname`、`you@example.com`） |
| 项目卡片 | `index.html` 里 `id="projects"` 那一段 |
| 笔记列表 | `index.html` 里 `id="notes"` 那一段 |
| 配色（主色紫 / 背景） | `style.css` 顶部 `:root` 里的 `--accent`、`--bg-1..3` |
| 头像 | `index.html` 里 `<div class="avatar">你</div>`，或换成 `<img src="avatar.jpg">` |

## 部署到 Cloudflare Pages

> **不需要备案。** Cloudflare 免费版走境外节点，备案只对"中国大陆境内节点"有要求。

### 方式 A：连 GitHub 仓库（推荐，push 即自动部署）

1. 把这个目录推到一个 GitHub 仓库（公开或私有都行）
2. 打开 <https://dash.cloudflare.com/> → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
3. 选中仓库，构建设置填：
   - Framework preset: **None**
   - Build command: **留空**
   - Build output directory: **/**（若仓库根目录就是这些文件）或 **website**
4. **Save and Deploy**，一分钟内拿到 `xxx.pages.dev` 地址

### 方式 B：直接上传（不用 git）

```bash
npm install -g wrangler
cd website
wrangler pages deploy . --project-name=mysite
```
第一次会打开浏览器让你登录 Cloudflare。

### 绑定自己的域名

Pages 项目 → **Custom domains** → **Set up a domain** → 填你的域名。
- 域名 DNS 已经在 Cloudflare：一键完成，SSL 自动签发
- 域名 DNS 在别处：按提示加一条 CNAME 记录

> ⚠️ 免费的 `*.pages.dev` 域名在国内经常打不开/很慢，**建议配自己的域名**（体验会好不少，但仍不如国内节点）。

## 以后想加的东西

- 博客：文件多了以后可以换成静态生成器（Astro / Hugo），仍是纯静态
- 评论：Waline / Twikoo（需要一个小后端）或 Giscus（基于 GitHub Discussions）
- 访问统计：Umami 或 Cloudflare Web Analytics（免费、无 Cookie）

## 已上线

- 生产地址：<https://homepage-9cw.pages.dev>
- 部署方式：`wrangler pages deploy`（Cloudflare Pages 直传模式）
- 更新流程（改完文件后）：

```bash
cd /d D:\RJ\website
git add -A && git commit -m "更新内容" && git push
wrangler pages deploy . --project-name=homepage --branch=main
```

> 注意：本项目是 **Direct Upload（直传）** 模式，Cloudflare 不允许事后改成 Git 关联模式；
> 若要 `git push` 自动部署，需新建一个 Git 关联项目，或在 GitHub Actions 里用 API Token 部署。