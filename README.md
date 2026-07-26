# 轻奢风格静态独立站

从 [xyfk-hltx3](https://github.com/zxmail/xyfk-hltx3) 项目抓取商品分类和商品数据，生成一个纯静态的独立站点（轻奢风格）。支持每12小时自动更新数据。

## 📦 项目结构

```
oue/
├── fetch-data.js       # 数据抓取脚本（调用源站 API）
├── generate-site.js    # 静态站生成器（JSON → HTML，轻奢风格）
├── build.sh            # 一键构建脚本
├── .env.example        # 环境变量模板
├── .env                # 你的环境变量（需创建）
├── data/               # 抓取的 JSON 数据（自动生成）
│   ├── config.json
│   ├── categories.json
│   ├── products.json
│   └── meta.json
└── dist/               # 生成的静态站（可直接部署）
    └── index.html
```

## 🚀 快速开始

### 方式一：GitHub Pages（推荐）

1. Fork 或上传本项目到你的 GitHub
2. 进入仓库 Settings → Pages → Source 选择 `gh-pages` 分支
3. 每12小时自动构建部署（GitHub Actions）
4. 手动触发：Actions → Build & Deploy → Run workflow

### 方式二：本地构建

```bash
SITE_URL=https://hltx.eu.cc ./build.sh
cd dist && python3 -m http.server 8080
```

## 🎨 设计风格

采用**轻奢风格**设计：
- 奶白暖色调背景
- 金色渐变点缀
- Playfair Display 优雅衬线字体
- 圆润卡片 + 精致阴影
- 响应式布局，移动端友好

## ⏰ 自动更新

GitHub Actions 配置为每天 0 点和 12 点（UTC 16:00 / 04:00）自动构建部署。

手动触发：Actions → Build & Deploy → Run workflow

## 🌐 部署建议

生成的 `dist/` 目录是纯静态文件，可部署到：
- **GitHub Pages** — 推送到 `gh-pages` 分支
- **Cloudflare Pages** — 拖拽上传或 Git 集成
- **Vercel** — `vercel --prod dist/`
- **Netlify** — 拖拽 `dist/` 文件夹

## 📝 注意事项

- 数据来源于原站 API，静态站不包含购买/支付功能
- 图片仍从原站加载（使用绝对路径）
- 生成的 HTML 文件支持 SEO（包含 OG 标签 + JSON-LD 结构化数据）
