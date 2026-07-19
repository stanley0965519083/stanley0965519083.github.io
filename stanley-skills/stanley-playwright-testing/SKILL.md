---
name: stanley-playwright-testing
description: Stanley 的 Playwright E2E 測試標準。Use this skill whenever the user wants to test a website, write E2E/integration tests, verify a web page works, automate a browser, or mentions Playwright, 測試網站, 自動化測試 — and after building any non-trivial website to verify critical flows before delivery.
---

# Stanley Playwright Testing — E2E 測試標準

用 Playwright 驗證網站關鍵流程。測試使用者感知的行為,不測實作細節。

## Locator 優先序(嚴格遵守)

1. getByRole(role, { name }) — 首選,同時驗證無障礙
2. getByLabel / getByPlaceholder — 表單欄位
3. getByText — 靜態內容
4. getByTestId — 刻意的逃生口
5. CSS/XPath — 最後手段,幾乎不用

role-based locator 能撐過重構,還兼做 a11y 檢查。

## 核心原則

- **web-first assertion**:await expect(locator).toBeVisible() — 自動重試,不會 flaky
- **刪除所有硬等待**:禁止 waitForTimeout;用條件等待(expect 自帶)
- **測試隔離**:每個測試獨立 context,絕不共享狀態、絕不依賴執行順序
- **fixtures 圍繞業務行為**建模(loginAs、createProject),不是包裝原始 API

## 認證模式(2026 標準做法)

專用 setup project 登入一次,存 storageState,所有測試直接載入:

```ts
// playwright.config.ts
projects: [
  { name: 'setup', testMatch: /auth\.setup\.ts/ },
  { name: 'e2e', use: { storageState: 'playwright/.auth/user.json' },
    dependencies: ['setup'] },
]
```

## 測試範圍(必測清單)

- 每個主要頁面:載入成功、無 console error、標題正確
- 關鍵流程:表單送出、導覽、購買/聯絡等轉換路徑
- 響應式:mobile viewport(375px)關鍵頁面可用
- 失敗路徑:表單驗證錯誤有正確提示

## 專案設定

```bash
npm init playwright@latest
```

- CI 上 headless、重試 2 次;本機 headed debug 用 --ui
- trace: 'on-first-retry' 方便查失敗原因
- 平行執行 fullyParallel: true

## 與 Playwright MCP 的分工

- Playwright MCP(對話中):互動式操作、探索、快速驗證、截圖
- Playwright 測試(程式碼):可重複執行的回歸保障,交付進 repo
