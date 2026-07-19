---
name: stanley-core-web-vitals
description: Stanley 的網站效能優化手冊(Core Web Vitals:LCP/INP/CLS)。Use this skill whenever the user mentions website performance, page speed, Lighthouse, 網站很慢, 效能優化, or when building/finishing ANY website — performance must be verified before delivery because Google's 2026 algorithm weights performance heavily.
---

# Stanley Core Web Vitals — 效能優化手冊

2026 年 3 月起 Google 演算法加重效能權重;通過全部三項指標的網站跳出率低 24%。任何網站交付前必須通過。

## 三大指標門檻(必須全綠)

| 指標 | 門檻 | 意義 |
|---|---|---|
| LCP | < 2.5s | 最大內容繪製 |
| INP | < 200ms | 互動到下一次繪製(43% 網站不及格,最常見死因) |
| CLS | < 0.1 | 版面位移 |

## LCP 優化(四大高影響修法)

1. **LCP 圖片預載**:link rel="preload" as="image";LCP 圖片**絕不** lazy load,加 fetchpriority="high"
2. **關鍵 CSS inline**,其餘延後
3. **字體 preload + font-display: swap**(next/font 自動處理)
4. **SSR/SSG 輸出**,不要 client-side render 首屏

圖片規則:AVIF/WebP、精確尺寸、非首屏才 lazy、上 CDN。

## INP 優化(主因:JS 阻塞主執行緒)

- 長任務切塊:超過 50ms 的工作用 setTimeout / scheduler.yield() 讓出主執行緒
- 互動回饋先行:點擊先更新 UI(樂觀更新),重運算丟 Web Worker
- 減少 client JS:能用 Server Component 就不要 hydrate
- 第三方腳本:next/script 用 strategy="lazyOnload";分析工具延後載入

## CLS 優化

- 所有圖片/影片/廣告位:明確 width/height 或 aspect-ratio
- 字體 swap 位移:用 size-adjust 或 next/font
- 動態內容(banner、cookie 條)預留空間,絕不往下推擠內容

## 驗證流程(交付前必跑)

```bash
npm run build && npm run start
npx lighthouse http://localhost:3000 --view
```

目標:Performance >= 90、三項 CWV 全綠。未達標時回到對應章節逐項修再測。有 Playwright MCP 時可直接實測互動延遲。
