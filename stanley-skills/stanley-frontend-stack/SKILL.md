---
name: stanley-frontend-stack
description: Stanley 的現代前端技術棧標準(Next.js 15 + React 19 + TypeScript + Tailwind v4 + shadcn/ui)。Use this skill whenever the user wants to create, scaffold, or refactor a web project/app — including 建網站專案、開新專案、寫個 web app、React 專案 — so structure, stack choices, and conventions follow Stanley's standard instead of ad-hoc choices.
---

# Stanley Frontend Stack — 專案技術棧標準

建立新網站專案時,一律採用此標準組合與結構。

## 標準技術棧(2026)

| 層 | 選擇 | 原因 |
|---|---|---|
| 框架 | Next.js 15+(App Router) | SSR/SSG/ISR 混合渲染,Core Web Vitals 友善 |
| UI | React 19 + TypeScript(strict) | React Compiler 自動 memo;TS 大幅減少 debug 時間 |
| 樣式 | Tailwind CSS v4(Oxide 引擎) | 建置快 10 倍;production CSS 極小 |
| 元件庫 | shadcn/ui | 可完全客製、複製進專案、無黑盒依賴 |
| 狀態 | Zustand(client)+ Server Components(server) | 輕量;優先用伺服器狀態 |

例外:小型單頁(作品集單頁、活動頁)直接用單一 HTML 檔 + Tailwind,不要過度工程。

## 專案結構(App Router)

```
app/
  layout.tsx        # 全域 layout、字體、metadata
  page.tsx          # 首頁(Server Component)
  globals.css       # @import "tailwindcss"; + design tokens
components/
  ui/               # shadcn/ui 元件
  sections/         # Hero、Features 等區塊元件
lib/                # 工具函式
public/             # 靜態資源
```

## 核心慣例

- **預設 Server Component**;需要互動/hook 才加 "use client",且下推到葉節點
- 圖片一律 next/image;字體一律 next/font(自動 self-host、防 CLS)
- 資料抓取在 Server Component 內 async/await,不要 useEffect fetch
- TypeScript strict: true;禁止 any,不確定就 unknown + 收窄
- 環境變數:僅 NEXT_PUBLIC_ 前綴可進 client;秘密永不進 client bundle
- 每個元件單一職責;超過 150 行就拆

## Tailwind v4 要點

- CSS-first 設定:在 globals.css 用 @theme 定義 tokens,不再用 tailwind.config.js
- 用語意化 token:--color-primary,而非到處寫死 blue-500
- 響應式 mobile-first:先寫手機樣式,再加 md: lg:

## 建立專案指令

```bash
npx create-next-app@latest my-site --typescript --tailwind --eslint --app
npx shadcn@latest init
```

## 品質門檻(交付前自檢)

1. npm run build 零錯誤零警告
2. 首頁 Lighthouse Performance >= 90(見 stanley-core-web-vitals)
3. 視覺符合 stanley-web-design-2026
4. 無障礙符合 stanley-accessibility-wcag
