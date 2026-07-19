---
name: stanley-seo-technical
description: Stanley 的技術 SEO 檢查表(metadata、JSON-LD 結構化資料、sitemap)。Use this skill whenever the user builds or updates any public-facing website or page, mentions SEO, Google 排名, 搜尋曝光, meta tags, or sitemap — every deliverable website must ship with correct SEO scaffolding, even if the user didn't explicitly ask for SEO.
---

# Stanley Technical SEO — 技術 SEO 標準配備

任何對外網站交付時,以下項目為標準配備,不需使用者另外要求。

## Metadata(每頁必備)

Next.js 用 Metadata API;純 HTML 直接寫 head:

- title:50-60 字元,「主關鍵字 | 品牌名」
- meta description:120-155 字元,含行動誘因
- lang="zh-Hant-TW"(繁中站)/ 正確語言標記
- canonical URL
- Open Graph 全套:og:title、og:description、og:image(1200x630)、og:url、og:type
- Twitter Card:summary_large_image

## 結構化資料 JSON-LD

依網站類型加入對應 schema(放 script type="application/ld+json"):

- 企業/工作室 → Organization + WebSite
- 個人作品集 → Person
- 文章/部落格 → Article(含 datePublished、author)
- 商品頁 → Product + Offer
- FAQ 區塊 → FAQPage

## 網站層級檔案

- sitemap.xml(Next.js 用 app/sitemap.ts 自動生成)
- robots.txt(app/robots.ts);開發/預覽環境要 noindex
- favicon + apple-touch-icon + manifest

## 內容結構規則

- 每頁**恰好一個** h1;標題階層不跳級(h1→h2→h3)
- 語意化標籤:main、nav、article、footer
- 圖片 alt 必填且具描述性(同時是 WCAG 要求)
- 內部連結用描述性文字,不用「點這裡」

## 2026 重點

- **效能即 SEO**:Core Web Vitals 直接影響排名(見 stanley-core-web-vitals)
- AI 搜尋(AI Overviews)偏好:清楚標題階層、FAQ 結構、可引用的段落式答案
- 行動版優先索引:mobile 版內容必須完整

## 交付前檢查

1. 每頁 title/description 不重複
2. npx lighthouse SEO 分數 >= 95
3. JSON-LD 用 Google Rich Results Test 驗證通過
