---
name: stanley-responsive-ui
description: Stanley 的響應式 UI 實作標準(RWD、container queries、流體字級)。Use this skill whenever implementing any web layout, fixing mobile display issues, or the user mentions RWD, 響應式, 手機版, breakpoints, 排版跑掉 — every website must be mobile-first and fluid, not fixed-width.
---

# Stanley Responsive UI — 響應式實作標準

所有網站以 mobile-first 開發:先寫手機樣式,往上加斷點。

## 斷點策略(Tailwind 預設)

| 斷點 | 寬度 | 目標 |
|---|---|---|
| (預設) | < 640px | 手機直向 |
| sm | 640px | 手機橫向 |
| md | 768px | 平板 |
| lg | 1024px | 筆電 |
| xl | 1280px | 桌機 |

原則:內容決定斷點。排版壞了才加斷點,不是為裝置清單寫死。

## 流體優先(能不寫斷點就不寫)

- 字級:clamp(1rem, 0.5rem + 1.5vw, 1.25rem);Hero 標題 clamp(2.5rem, 8vw, 6rem)
- 間距:clamp() 或 CSS 變數階梯
- 版面:grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)) — 卡片自動換行免斷點
- 圖片:max-width: 100%; height: auto; + aspect-ratio 防 CLS

## Container Queries(元件級響應)

元件依「容器寬度」而非視窗寬度變化 — 同一卡片在側欄窄容器與主欄寬容器自動切換版型:

```css
.card-wrap { container-type: inline-size; }
@container (min-width: 400px) { .card { display: flex; } }
```

Tailwind v4:@container 與 @lg: 前綴原生支援。

## 行動端必檢清單

- 觸控目標 >= 44x44px,間距足夠(拇指友善)
- viewport meta:width=device-width, initial-scale=1(禁止 user-scalable=no)
- 橫向捲動 = bug:檢查 overflow-x,找出爆寬元素
- 固定 header 在手機上不可吃掉超過 15% 高度
- 表單:正確 inputmode / type(email、tel)喚起對的鍵盤
- iOS Safari:注意 100vh 問題,用 100dvh

## Bento Grid 響應式模式(搭配 stanley-web-design-2026)

```css
.bento { display: grid; gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr)); }
.bento > .featured { grid-column: span 2; } /* 大卡片,手機自動降為單欄 */
```

## 驗證

- DevTools 裝置模擬:375px、768px、1440px 三檔全檢查
- 有 Playwright 時:三種 viewport 各截圖比對
