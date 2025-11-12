# 課程三：MoksaWP - 佈景主題與外掛開發 (導覽頁)

哈囉，歡迎來到 MoksaWP 的第三階段課程：「佈景主題與外掛開發」。

我是你在這堂課的導師。首先，我要恭喜你，踏入這個章節，代表你已經準備好**從 WordPress 的「使用者」蛻變為「創造者」**。這是一趟充滿挑戰但回報豐碩的旅程，你將不再受限於現成的佈景主題或外掛，而是能夠親手打造完全符合客戶需求、兼具效能與擴充性的客製化網站。

這門長達 50 小時的深度課程，將帶你從開發環境的建置開始，一步步深入 WordPress 的核心，最終讓你具備獨立開發商業級佈景主題與外掛的專業能力。

---

### 課程目標

這門課不是紙上談兵。我們的目標非常明確，在課程結束時，你將能夠：

1.  **獨立建置專業開發環境**：使用 LocalWP、VS Code 與 Git 進行高效、可控的開發。
2.  **精通 WordPress 核心運作**：徹底理解 Template Hierarchy (範本層級)、Hooks (掛鉤：Action & Filter) 與 The Loop (主循環)，這是所有開發的基礎。
3.  **從零到一開發客製化佈景主題**：包含傳統的 Classic Theme 與現代的 Block Theme (區塊佈景主題)。
4.  **開發實用的客製化外掛**：學會建立 Custom Post Types (CPT)、Custom Fields (ACF) 並將商業邏輯封裝成可重複使用的外掛。
5.  **掌握 Gutenberg 區塊開發**：使用 React (JavaScript) 開發你自己的客製化區塊，跟上 WordPress 的最新趨勢。
6.  **串接 API 與自動化**：學會使用 WordPress REST API 與 WP-CLI，讓你的網站能與外部服務溝通，並透過指令碼進行高效管理。
7.  **實踐 WooCommerce 的進階客製化**：開發客製化的金流、物流或特殊折扣功能，滿足複雜的電商需求。

---

### Moksa 的開發哲學：不只是寫 Code

在 Moksa，我們強調的不僅僅是「寫出能動的程式碼」。我們將遵循業界的最佳實踐，建立一套專業、可維護、高效能的開發工作流程。

*   **版本控制是標配**：我們所有的專案都會使用 **Git** 進行版本控制，確保每一次的修改都有跡可循，團隊協作更加順暢。
*   **本地開發優先**：我們將使用 **LocalWP** 在你的電腦上建立一個安全、快速且獨立的開發環境，告別直接在線上主機修改程式碼的風險。
*   **遵循官方編碼標準**：你的程式碼不僅要能運作，更要易於閱讀與維護。我們將遵循 **WordPress Coding Standards**。
*   **效能是第一考量**：從資料庫查詢到前端資源載入，我們將使用 **Query Monitor** 等工具，隨時監控並優化程式碼的效能。
*   **安全是基本要求**：學習如何對使用者的輸入進行清理 (Sanitization) 與轉義 (Escaping)，從源頭杜絕安全漏洞。

---

### 課程單元總覽

這 50 小時的課程將分為以下幾個主要單元：

#### **單元一：開發環境與核心基礎 (約 8 小時)**
*   1.1 (實作) 安裝與設定專業開發工具 (LocalWP, VS Code, Git)
*   1.2 (觀念) 深入理解 WordPress 檔案結構與資料庫
*   1.3 (觀念) WordPress 運作核心：Template Hierarchy 範本層級詳解
*   1.4 (觀念) WordPress 的魔法：徹底搞懂 Hooks (Actions 與 Filters)
*   1.5 (實作) 你的第一個 Child Theme (子佈景主題)
*   1.6 (工具) WP-CLI 入門：用命令列管理 WordPress

#### **單元二：客製化佈景主題開發 (約 12 小時)**
*   2.1 (實作) 從 `_s` (Underscores) 開始你的 Classic Theme
*   2.2 (實作) `functions.php` 的妙用：註冊導覽選單、側邊欄與圖片尺寸
*   2.3 (實作) 使用 Template Parts 組織你的程式碼
*   2.4 (實作) 整合 Advanced Custom Fields (ACF) 打造彈性頁面
*   2.5 (觀念) 現代化趨勢：Block Theme 區塊佈景主題與 `theme.json`
*   2.6 (實作) 打造一個簡易的 FSE (Full Site Editing) 佈景主題

#### **單元三：客製化外掛開發 (約 12 小時)**
*   3.1 (實作) 你的第一個外掛：檔案結構與 Plugin Headers
*   3.2 (觀念) Activation/Deactivation Hooks：外掛啟用與停用的生命週期
*   3.3 (實作) 建立 Custom Post Types (CPT) 與 Custom Taxonomies
*   3.4 (實作) 使用 Shortcodes 讓使用者輕鬆嵌入動態內容
*   3.5 (實作) 建立後台設定頁面 (Settings API)
*   3.6 (實作) 整合 WooCommerce：為商品頁面增加客製化欄位

#### **單元四：Gutenberg 區塊開發 (約 10 小時)**
*   4.1 (觀念) JavaScript 在 WordPress 中的角色與 modern toolchain (Node.js, npm, Webpack)
*   4.2 (觀念) React 基礎入門 for WordPress 開發者
*   4.3 (實作) 使用 `@wordpress/create-block` 快速建立你的第一個區塊
*   4.4 (實作) 深入 `block.json` 與區塊屬性 (Attributes)
*   4.5 (實作) `edit.js` 與 `save.js`：打造區塊的後台編輯與前台顯示
*   4.6 (實作) 打造一個可重複使用的「推薦引言」區塊

#### **單元五：進階主題與部署 (約 8 小時)**
*   5.1 (觀念) WordPress REST API 入門與實踐
*   5.2 (實作) 建立你自己的 Custom REST API Endpoints
*   5.3 (實作) WooCommerce 進階：客製化一個綠界金流的提示訊息
*   5.4 (觀念) 國際化 (i18n) 與在地化 (l10n)：讓你的主題/外掛支援多國語系
*   5.5 (實務) 專案部署流程：使用 Git 將本地專案部署到線上主機
*   5.6 (總結) 專案上架與維護的最佳實踐

---

### 在開始之前

這是一門進階課程，我們假設你已經具備以下基礎：

*   熟悉 WordPress 後台操作 (已完成 MoksaWP 課程一)。
*   具備 **HTML** 與 **CSS** 的基礎知識。
*   具備 **PHP** 的基本語法知識 (了解變數、陣列、迴圈、函式)。
*   對 **JavaScript** 有初步的認識 (非必要，但強烈建議)。

準備好了嗎？這將是你 WordPress 技能樹中，最重要、也最有價值的一次升級。

讓我們開始這趟精彩的開發之旅吧！