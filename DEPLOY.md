# 部署命令参考（任选一家）

本目录是纯静态站点，零后端依赖，可直接丢到 Vercel 或 Cloudflare Pages。

## 文件说明
- `index.html`    —— 客户入口（公开，上传 Excel 自动扫描，物理不含后台）
- `advisor.html`  —— 顾问入口（口令 `xiaoshan2026` 解锁处置手册 + 粘贴咨询码还原）
- `xlsx.full.min.js` —— 本地 SheetJS，浏览器端解析 Excel，不上传服务器

## 一、Vercel
### 方式 A：有 Deploy Token（交给 AI 推）
```bash
vercel deploy --prod --prebuilt --token <VERCEL_TOKEN> --name tax-risk-scanner .
```
### 方式 B：本地 CLI
```bash
npm i -g vercel
vercel login            # 浏览器授权
vercel                  # 首次，按提示链接项目，输出预览 URL
vercel deploy --prod    # 上线，根目录即本文件夹
```

## 二、Cloudflare Pages
### 方式 A：有 API Token（交给 AI 推）
```bash
CLOUDFLARE_API_TOKEN=<CF_TOKEN> CLOUDFLARE_ACCOUNT_ID=<ACCOUNT_ID> \
  npx wrangler pages deploy . --project-name tax-risk-scanner
```
### 方式 B：本地 CLI
```bash
npm i -g wrangler
wrangler login          # 浏览器授权
wrangler pages deploy . --project-name tax-risk-scanner
```

## 三、GitHub 推送自动部署（推荐长期方案）
1. 把本目录内容推到一个 GitHub 仓库。
2. Vercel / Cloudflare Pages 后台「Import Git Repo」→ 选该仓库 → Framework 选 None / Static → 直接部署。
3. 之后每次 git push 自动重新上线，无需本地 CLI。

## 上线后的访问方式（与平台无关）
- 客户入口：站点根地址 `/`（如 https://tax-risk-scanner.vercel.app/）
- 顾问入口：站点 `/advisor`（如 https://tax-risk-scanner.vercel.app/advisor），口令 `xiaoshan2026`
- 客户用「生成咨询码」把结果发你微信 → 你在顾问版「粘贴客户咨询码」还原并出处置手册
