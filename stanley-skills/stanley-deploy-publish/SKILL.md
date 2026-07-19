---
name: stanley-deploy-publish
description: Stanley 的網站部署發佈流程(GitHub Pages / Vercel / Netlify)。Use this skill whenever the user wants to deploy, publish, ship, or go live with a website, mentions 部署, 上線, 發佈網站, GitHub Pages, Vercel, or Netlify — including updating Stanley's own site stanley0965519083.github.io.
---

# Stanley Deploy & Publish — 部署發佈流程

依專案類型選平台,一律走 Git 部署(不手動拖檔案)。

## 平台選擇

| 情境 | 平台 | 原因 |
|---|---|---|
| 靜態站/作品集 | GitHub Pages | Stanley 已有 stanley0965519083.github.io |
| Next.js 全功能 | Vercel | 原生支援 SSR/ISR,零設定 |
| 靜態 + 表單/函式 | Netlify | 內建表單處理與 edge functions |

## Git 流程(共通,使用全域身分)

```bash
git init                      # 若尚未是 repo(預設分支 main)
git add -A
git commit -m "feat: initial site"
git remote add origin https://github.com/stanley0965519083/<repo>.git
git push -u origin main
```

規則:main 分支即生產;敏感資訊(.env)絕不入 repo(.gitignore 先行);commit 訊息用 conventional commits(feat:/fix:/chore:)。

## GitHub Pages(個人站 stanley0965519083.github.io)

- 個人主站 repo 名必須是 stanley0965519083.github.io,push main 即上線
- 專案站:repo Settings → Pages → Source 選 GitHub Actions
- Next.js 靜態化:next.config.ts 設 output: 'export';專案站需設 basePath: '/<repo>'
- 自訂網域:加 CNAME 檔 + DNS 設定,啟用 Enforce HTTPS

## Vercel

- 用 Vercel MCP 連接器或網頁匯入 GitHub repo,main push 自動部署
- PR 自動產生 Preview 部署,先看預覽再合併
- 環境變數在 Vercel 後台設定,分 Production/Preview/Development

## Netlify

- 連接 GitHub repo;build command 與 publish dir 依框架自動偵測
- 表單:form 標籤加 data-netlify="true" 即收單

## 上線前檢查(全部通過才 push)

1. npm run build 成功、本地 preview 正常
2. stanley-core-web-vitals:Lighthouse >= 90
3. stanley-seo-technical:metadata/sitemap/robots 齊全
4. stanley-accessibility-wcag:a11y >= 95
5. 404 頁面存在;所有內部連結有效

## 上線後驗證

- 實際網址開一次(不是 localhost);檢查 HTTPS 鎖頭
- Google Search Console 提交 sitemap
