---
name: stanley-web-design-2026
description: Stanley 的現代網站視覺設計指南(2026 設計趨勢)。Use this skill whenever the user asks to design, build, redesign, or style ANY website, landing page, portfolio, or web UI — even if they only say 做一個網站、幫我設計網頁、landing page、官網 — to make the result look modern and professional instead of generic. Covers bento grid layout, typography, color systems, glassmorphism, motion.
---

# Stanley Web Design 2026 — 現代網站視覺設計

建立任何網站時,套用以下 2026 現代設計原則,避免做出「AI 樣板感」的通用頁面。

## 設計方向選擇(先問或先判斷)

依品牌屬性二選一,不要混用:

1. **Dopamine / Y2K 風**:高飽和色、霓虹漸層、高對比配色 — 適合生活風格、美妝、年輕族群品牌
2. **溫暖大地風**:低視覺疲勞的大地色系、米白底、暖棕/橄欖綠點綴 — 適合企業、工作室、專業服務

## 版面 Layout

- **Bento Grid(便當盒格線)為預設首選**:模組化卡片、大小交錯、圓角 16-24px
- 打破完美矩形:有機形狀、blob、波浪分隔線、不對稱容器
- 大量留白;區塊間距至少 96px(desktop)/ 48px(mobile)
- 每頁一個明確視覺焦點,避免所有區塊搶眼

## 字體 Typography(2026 重點:字體即主角)

- 標題超大化:Hero 標題 clamp(2.5rem, 8vw, 6rem),粗細 700-900
- 標題用有個性的展示型/可變字體,內文用高可讀字體;正文 16-18px、行高 1.6-1.7
- 中文網站:標題 Noto Sans TC 900;避免細明體
- 可加動態文字(kinetic type):進場位移 + 淡入即可,不要過度

## 色彩系統

- 用 CSS 變數定義 design tokens:--color-primary、--color-surface、--color-text
- 對比度必須 >= 4.5:1(內文)、3:1(大字)— 同時是 WCAG 要求
- 漸層:同色相相鄰漸層(藍到紫)比對比色漸層安全
- 深色模式從一開始就設計,不要事後補

## 質感元素

- **Glassmorphism**:backdrop-filter: blur(12px) + 半透明背景 + 1px 淺邊框,用於導覽列與浮動卡片
- 微妙 3D / 陰影:多層柔和陰影(小 + 大),不用硬陰影
- 微互動:hover 時 scale(1.02) + 陰影加深,transition 200-300ms ease

## 動效原則

- 進場動畫用 IntersectionObserver 觸發,單次、150-400ms
- 尊重 prefers-reduced-motion,提供靜態替代
- 動效永遠不可阻擋操作或拖慢 LCP/INP(見 stanley-core-web-vitals)

## 禁止清單(AI 樣板感來源)

- 紫色漸層 hero + 三欄圖示卡片 + 置中大按鈕的萬用模板
- Lorem ipsum、無意義的 stock 圖示堆疊
- 過量 emoji 當設計元素
- 一頁塞十種顏色、五種字體
