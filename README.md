# 轻奢风格静态独立站

从 [xyfk-hltx3](https://github.com/zxmail/xyfk-hltx3) 项目抓取商品分类和商品数据，生成一个纯静态的独立站点。采用轻奢风格设计，支持自动部署和手动部署。

---

## 📦 项目文件说明

```
├── fetch-data.js           # 数据抓取脚本（从源站 API 拉取商品数据）
├── generate-site.js        # 静态站生成器（JSON → HTML，轻奢风格）
├── build.sh                # 一键构建脚本（自动调用上面两个）
├── seo.json                # SEO 配置文件（标题、描述、关键词等，可直接修改）
├── .env.example            # 环境变量模板
├── .gitignore              # Git 忽略规则
├── .github/workflows/
│   └── build.yml           # GitHub Actions 自动构建部署配置
├── index.html              # 构建生成的网站页面（自动生成，无需手动创建）
├── data/                   # 抓取的商品 JSON 数据（构建时自动生成）
│   ├── config.json         # 站点配置
│   ├── categories.json     # 商品分类
│   ├── products.json       # 商品列表
│   └── meta.json           # 元数据
└── dist/                   # 构建输出目录（构建时自动生成）
    └── index.html          # 生成的静态页面
```

### 核心文件（必须保留）

| 文件 | 作用 |
|------|------|
| `fetch-data.js` | 从源站 API 抓取商品分类和商品数据 |
| `generate-site.js` | 将 JSON 数据生成 HTML 静态页面（轻奢风格） |
| `build.sh` | 一键构建脚本，串联抓取和生成两个步骤 |
| `seo.json` | SEO 配置，修改标题、描述、关键词等直接编辑此文件 |

### 自动生成的文件（无需手动管理）

| 文件 | 说明 |
|------|------|
| `index.html` | 构建后自动生成的网站页面 |
| `data/` | 构建时自动抓取的商品数据 |
| `dist/` | 构建时自动生成的输出目录 |

---

## 🎨 设计风格

采用**轻奢风格**设计：
- 奶白暖色调背景（`#faf8f5`）
- 金色渐变点缀（`#b8965a` → `#d4b478`）
- Playfair Display 优雅衬线标题字体
- 圆润卡片 + 精致微阴影
- 完整响应式布局，移动端友好
- 兼容老版本浏览器（搜狗等）

---

## 🔍 SEO 说明

所有 SEO 配置集中在 `seo.json` 文件中，包含：

| 配置项 | 说明 |
|--------|------|
| `title` | 网站标题 |
| `titleSuffix` | 标题后缀（显示在浏览器标签页） |
| `description` | 网站描述（搜索结果摘要） |
| `keywords` | 关键词（逗号分隔） |
| `canonical` | 规范链接地址 |
| `og` | Open Graph 社交分享标签（Facebook/微信等） |
| `twitter` | Twitter 卡片标签 |
| `jsonLd` | JSON-LD 结构化数据（Google 搜索增强） |
| `favicon` | 网站图标 |

**修改方法：** 直接编辑 `seo.json`，保存后自动构建生效。

---

## 🚀 自动部署（GitHub Actions，推荐）

### 前提条件

1. 拥有 GitHub 账号
2. 仓库已创建（如 `hgudse.github.io`）
3. 仓库中包含本项目的所有文件

### 部署步骤

#### 第一步：设置 GitHub Pages

1. 打开仓库页面 → **Settings** → **Pages**
2. **Source** 选择 **Deploy from a branch**
3. **Branch** 选择 **`main`**，文件夹选 **`/ (root)`**
4. 点击 **Save**

#### 第二步：等待自动构建

GitHub Actions 会自动运行，流程如下：

```
代码推送到 main 分支
       ↓
GitHub Actions 触发
       ↓
运行 build.sh
  ├─ fetch-data.js → 从源站 API 抓取数据
  └─ generate-site.js → 生成 index.html
       ↓
将 index.html 提交到 main 分支
       ↓
GitHub Pages 自动部署
       ↓
网站上线 ✅
```

#### 自动更新频率

- 每天自动构建 2 次（UTC 04:00 和 16:00，即北京时间 12:00 和 00:00）
- 每次推送到 main 分支也会触发构建
- 可手动触发：**Actions** → **Build & Deploy** → **Run workflow**

### 访问地址

- 用户名为 `xxx`，仓库名为 `xxx.github.io` → 访问 `https://xxx.github.io`
- 用户名为 `xxx`，仓库名为其他名称 → 访问 `https://xxx.github.io/仓库名/`

---

## 🔧 手动部署（本地构建）

### 前提条件

1. 已安装 Node.js（版本 18 或以上）
2. 已安装 Git

### 部署步骤

#### 第一步：克隆仓库

```bash
git clone https://github.com/你的用户名/你的仓库名.git
cd 你的仓库名
```

#### 第二步：构建

```bash
# 设置数据源地址并构建
SITE_URL=https://hltx.eu.cc bash build.sh
```

构建完成后会输出：
```
>> Fetching data from https://hltx.eu.cc
>> Generating site
>> Done. Files in dist/
```

#### 第三步：本地预览（可选）

```bash
cd dist
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

#### 第四步：上传部署

**方式 A：推送到 GitHub（自动触发 Pages 部署）**

```bash
git add -A
git commit -m "rebuild"
git push origin main
```

**方式 B：手动上传 index.html**

1. 将 `dist/index.html` 的内容复制到仓库根目录的 `index.html`
2. 在 GitHub 网页端上传，或用 Git 推送

---

## ❓ 常见问题

### Q: 打开网站显示 404？

**A:** 检查以下设置：
1. **Settings → Pages → Source** 是否选择了 `main` 分支
2. 仓库名是否为 `用户名.github.io`（如果是其他名称，访问地址为 `用户名.github.io/仓库名/`）
3. Actions 是否构建成功（**Actions** 页面查看状态）

### Q: 修改了 seo.json 但没生效？

**A:** 等待 Actions 自动构建完成（约 2-3 分钟），或手动触发：**Actions** → **Run workflow**

### Q: 如何更换数据源？

**A:** 修改 `.github/workflows/build.yml` 中的 `SITE_URL` 环境变量，或本地构建时更改 `SITE_URL` 参数。

### Q: 如何修改网站风格？

**A:** 编辑 `generate-site.js` 中的 CSS 部分（以 `const CSS = \` 开头的区域）。

### Q: 数据安全吗？暴露 API 接口有风险吗？

**A:** 安全。`seo.json` 和代码中涉及的 API 接口（`/api/shop/config`、`/api/shop/categories`、`/api/shop/products`）都是原站前端公开调用的只读接口，任何人访问原站按 F12 都能看到，不存在额外安全风险。

---

## 📋 数据源 API 说明

本项目使用以下公开 API（由源站提供）：

| 接口 | 说明 |
|------|------|
| `GET /api/shop/config` | 站点配置（名称、Logo 等） |
| `GET /api/shop/categories` | 商品分类列表 |
| `GET /api/shop/products` | 所有上架商品（含规格和价格） |

---

## 🌐 可部署平台

生成的 `index.html` 是纯静态文件，可部署到任何静态托管服务：

| 平台 | 说明 |
|------|------|
| **GitHub Pages** | 免费，支持自动部署（本项目默认方式） |
| **Cloudflare Pages** | 免费，全球 CDN 加速 |
| **Vercel** | 免费，`vercel --prod dist/` |
| **Netlify** | 免费，拖拽上传 |
| **Nginx** | 自建服务器，`root /path/to/dist;` |
| **阿里云 OSS / 腾讯云 COS** | 国内云存储静态网站托管 |

---

## 📝 更新日志

- **2026-07-26** — 初始版本，轻奢风格，SEO 独立配置
