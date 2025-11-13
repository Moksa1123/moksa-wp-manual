# MoksaWP 第三階段課程：佈景主題與外掛開發 (導覽頁)

哈囉，歡迎來到 MoksaWP 的第三階段課程：「佈景主題與外掛開發」。

我是你在這堂課的導師。首先，我要恭喜你，踏入這個章節，代表你已經準備好從 WordPress 的「使用者」蛻變為「創造者」。這是一趟充滿挑戰但回報豐碩的旅程，你將不再受限於現成的佈景主題或外掛，而是能夠親手打造完全符合客戶需求、兼具效能與擴充性的客製化網站。

這門長達 50 小時的深度課程，將帶你從開發環境的建置開始，一步步深入 WordPress 的核心，最終讓你具備獨立開發商業級佈景主題與外掛的專業能力。

---

## 課程目標

這門課不是紙上談兵。我們的目標非常明確，在課程結束時，你將能夠：

*   **獨立建置專業開發環境：** 使用 LocalWP、VS Code 與 Git 進行高效、可控的開發。
*   **精通 WordPress 核心運作：** 徹底理解 Template Hierarchy (範本層級)、Hooks (掛鉤：Action & Filter) 與 The Loop (主循環)，這是所有開發的基礎。
*   **從零到一開發客製化佈景主題：** 包含傳統的 Classic Theme 與現代的 Block Theme (區塊佈景主題)。
*   **開發實用的客製化外掛：** 學會建立 Custom Post Types (CPT)、Custom Fields (ACF) 並將商業邏輯封裝成可重複使用的外掛。
*   **掌握 Gutenberg 區塊開發：** 使用 React (JavaScript) 開發你自己的客製化區塊，跟上 WordPress 的最新趨勢。
*   **串接 API 與自動化：** 學會使用 WordPress REST API 與 WP-CLI，讓你的網站能與外部服務溝通，並透過指令碼進行高效管理。
*   **實踐 WooCommerce 的進階客製化：** 開發客製化的金流、物流或特殊折扣功能，滿足複雜的電商需求。

---

## Moksa 的開發哲學：不只是寫 Code

在 Moksa，我們強調的不僅僅是「寫出能動的程式碼」。我們將遵循業界的最佳實踐，建立一套專業、可維護、高效能的開發工作流程。

*   **版本控制是標配：** 我們所有的專案都會使用 Git 進行版本控制，確保每一次的修改都有跡可循，團隊協作更加順暢。
*   **本地開發優先：** 我們將使用 LocalWP 在你的電腦上建立一個安全、快速且獨立的開發環境，告別直接在線上主機修改程式碼的風險。
*   **遵循官方編碼標準：** 你的程式碼不僅要能運作，更要易於閱讀與維護。我們將遵循 WordPress Coding Standards。
*   **效能是第一考量：** 從資料庫查詢到前端資源載入，我們將使用 Query Monitor 等工具，隨時監控並優化程式碼的效能。
*   **安全是基本要求：** 學習如何對使用者的輸入進行清理 (Sanitization) 與轉義 (Escaping)，從源頭杜絕安全漏洞。

---

## 課程單元總覽

這 50 小時的課程將分為以下幾個主要單元，嚴格按照您提供的順序與標題：

### 01. 開發環境與核心基礎

*   01.01 課程介紹 (從開發者角度看 WordPress)
*   01.02 本地端開發 (LocalWP, Docker)
*   01.03 開發工具 (VS Code, WP-CLI, Query Monitor)
*   01.04 (實務) 版本控制 (Git) 與 GitHub 流程
*   01.05 WordPress 檔案結構與資料庫結構 (wp_posts, wp_options)

### 02. 前端開發基礎

*   02.01 語意化 HTML5
*   02.02 CSS 核心 (Flexbox, Grid, RWD 設計模式)
*   02.03 SASS/SCSS (變數、Mixin、編譯)
*   02.04 (實作) 如何在 WordPress 正確引入 (Enqueue) CSS/JS
*   02.05 JavaScript (ES6+) 核心 (DOM 操作、Fetch API)
*   02.06 (實務) jQuery 在 WordPress 中的角色
*   02.07 (實務) 使用 NPM 與 Webpack 管理前端資源

### 03. PHP 與資料庫應用

*   03.01 PHP 基礎語法 (變數、陣列、迴圈、函式)
*   03.02 PHP 與 HTML 混編 (模板語法)
*   03.03 (實作) PHP 表單處理 (GET vs POST)
*   03.04 (實務) WordPress 中的 PHP (全域變數、常用函式)
*   03.05 SQL 查詢基礎 (SELECT, JOIN, WHERE)
*   03.06 (實作) WordPress 資料庫操作 ($wpdb)

### 04. 佈景主題結構與開發

*   04.01 佈景主題結構 (style.css, functions.php, index.php)
*   04.02 (核心) 模板層級 (Template Hierarchy)
*   04.03 (核心) The Loop (WP_Query) 詳解
*   04.04 (實作) 打造一個「子主題 (Child Theme)」
*   04.05 (實作) 打造一個「基本款」佈景主題 (Underscores, _s)
*   04.06 (實務) functions.php 的妙用 (註冊選單、側邊欄)

### 05. Hooks 核心觀念與進階應用

*   05.01 Hooks 核心觀念 (Action vs Filter)
*   05.02 (實作) add_action (在特定時間點「執行」)
*   05.03 (實作) add_filter (在特定時間點「修改」)
*   05.04 (實務) Hooks 進階 (優先權、自訂 Hook)
*   05.05 (實務) 如何使用 Query Monitor 追蹤 Hooks
*   05.06 (實務) WooCommerce 常用 Hooks (客製化結帳、商品頁)

### 06. 外掛開發基礎

*   06.01 外掛基礎結構 (外掛標頭)
*   06.02 (實作) 打造您的第一個外掛 (短代碼 Shortcode)
*   06.03 (實作) 建立外掛的「設定頁面」 (Options API)
*   06.04 (實務) 外掛的啟用 (Activation) 與停用 (Deactivation)
*   06.05 (實務) WP Cron (排程任務)
*   06.06 (實務) 國際化 (i18n) (讓您的外掛支援多國語言)

### 07. CPT, ACF 與 WooCommerce 進階客製化

*   07.01 (實作) 客製化「後台」 (CPT, Custom Post Type)
*   07.02 (實作) 客製化「後台欄位」 (ACF, Advanced Custom Fields)
*   07.03 (實作) (客製化金流) 串接「藍新 Pay」
*   07.04 (實作) (客製化物流) 串接「黑貓 API」

### 08. REST API 串接與外部整合

*   08.01 REST API 核心觀念 (JSON, Endpoints)
*   08.02 (實務) 使用 Postman 測試 WP API
*   08.03 (實作) 建立「自訂」的 API 端點 (register_rest_route)
*   08.04 (實務) API 驗證 (Nonce, JWT, 應用程式密碼)
*   08.05 (實作) (Headless) 使用 JS (React/Vue) 抓取 WP 資料

### 09. Gutenberg 區塊開發

*   09.01 Gutenberg 核心觀念 (Block, React, JSX)
*   09.02 (實作) 開發環境建置 (@wordpress/create-block)
*   09.03 (實作) 打造您的第一個「靜態 Block」
*   09.04 (實作) 打造您的第一個「動態 Block」 (ServerSideRender)
*   09.05 (實務) Block 的進階設定 (InspectorControls, RichText)
*   09.06 (實務) (進階) 打造一個「全站編輯 (FSE)」主題

### 10. AI 輔助開發

*   10.01 (觀念) AI 輔助開發的正確心態 (您是「指揮官」)
*   10.02 (實務) 使用 GitHub Copilot (VS Code) 加速開發
*   10.03 (實務) 如何「詠唱」(Prompt) AI 幫您寫 WP 程式碼 (PHP, Hooks)
*   10.04 (實務) (Gemini/Claude) 幫您除錯 (Debug)
*   10.05 (實務) (Google AI Studio) 串接 API (Gemini API)
*   10.06 (實作) 打造一個「AI 聊天機器人」外掛 (串接 Gemini API)

### 11. 網站效能、部署與現代化開發

*   11.01 (觀念) Headless WP (Gatsby, Next.js) 優缺點
*   11.02 (實務) 技術性 SEO 檢查清單 (Core Web Vitals)
*   11.03 (實作) (進階) Schema (使用 PHP/JSON-LD) 實作
*   11.04 (觀念) Programmatic SEO (程式化 SEO)

### 12. 進階維護與課程總結

*   12.01 (實務) WP Multisite (多站點) 網路
*   12.02 (實務) 自動化測試 (PHPUnit)
*   12.03 (實務) CI/CD 流程 (使用 GitHub Actions 自動部署)
*   12.04 (實務) 網站效能極限優化 (Redis, Object Cache)
*   12.05 課程總結 與 Q&A

---

## 學習前的準備

這是一門進階課程，我們假設你已經具備以下基礎：

*   熟悉 WordPress 後台操作 (已完成 MoksaWP 課程一)。
*   具備 HTML 與 CSS 的基礎知識。
*   具備 PHP 的基本語法知識 (了解變數、陣列、迴圈、函式)。
*   對 JavaScript 有初步的認識 (非必要，但強烈建議)。

準備好了嗎？這將是你 WordPress 技能樹中，最重要、也最有價值的一次升級。

讓我們開始這趟精彩的開發之旅吧！

---

## 附錄

*   **附錄 A：WP_Query 參數速查表**
*   **附錄 B：常用 Hooks (Action/Filter) 參考清單**
