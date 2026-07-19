---
name: stanley-accessibility-wcag
description: Stanley 的無障礙標準(WCAG 2.2 AA)。Use this skill whenever building or reviewing any website, form, or UI component — 94.8% of websites fail basic accessibility, and EU/US regulations now mandate WCAG 2.2 AA. Trigger on 無障礙, accessibility, a11y, WCAG, screen reader, or ANY website delivery even without explicit mention.
---

# Stanley Accessibility — WCAG 2.2 AA 標準

WCAG 2.2 是 2026 現行國際標準(EAA 與 ADA 皆要求 AA 級)。目標:**Level AA 全數通過**。

## 三大最常見失敗(先修這些)

1. **對比度不足**(1.4.3/1.4.11):內文 >= 4.5:1、大字 >= 3:1、UI 元件與圖形 >= 3:1
2. **alt 文字缺失**(1.1.1):有意義的圖片給描述性 alt;裝飾性圖片 alt=""
3. **表單缺 label**(1.3.1/3.3.2):每個輸入框都有可見 label 並用 for/id 關聯,不能只靠 placeholder

## POUR 四原則檢查表

**Perceivable 可感知**
- 影片有字幕;音訊有逐字稿
- 資訊不只靠顏色傳達(錯誤訊息加圖示與文字)
- 文字可放大 200% 不破版

**Operable 可操作**
- 全站鍵盤可完成:Tab 順序合理、focus 樣式明顯可見(不可 outline: none 不給替代)
- 目標尺寸 >= 24x24px(WCAG 2.2 新增 2.5.8)
- 拖曳操作提供替代方式(WCAG 2.2 新增 2.5.7)
- 無時間限制陷阱;無閃爍超過 3 次/秒的內容

**Understandable 可理解**
- html lang 正確;錯誤訊息說明如何修正
- 一致的導覽與求助入口(WCAG 2.2 新增 3.2.6)
- 不要求重複輸入相同資訊(WCAG 2.2 新增 3.3.7)

**Robust 穩健**
- 語意化 HTML 優先;ARIA 只在原生語意不足時使用
- 自訂元件(dropdown、modal、tabs)給正確 role、aria-expanded、焦點管理

## 實作模式

- Modal:開啟時焦點移入、Esc 關閉、焦點鎖在內部、關閉後焦點回觸發按鈕
- 跳過連結:頁首提供「跳到主要內容」
- 動態內容更新用 aria-live 通知
- prefers-reduced-motion 時停用動畫

## 驗證流程

1. 自動掃描:npx @axe-core/cli <url> 或 Lighthouse Accessibility >= 95
2. 鍵盤走一遍全部流程(不碰滑鼠)
3. 對比度用工具實測,不要目測
