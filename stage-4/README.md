# MoksaWP 第四階段課程：n8n與WordPress協作 (導覽頁)

哈囉！歡迎來到 MoksaWP 的第四階段課程：「n8n 與 WordPress 協作」。

恭喜你已完成了前面的課程，現在你已經掌握了 WordPress 的操作、設計與開發能力，能夠打造功能完善且高度客製化的網站。在這第四階段，我們將帶你進入「超自動化」的世界，學習如何利用強大的開源自動化工具 n8n，讓你的 WordPress 網站與各種服務無縫連接，實現前所未有的工作效率和使用者體驗。

這門長達 30 小時的深度實戰課程，將聚焦於 n8n 如何與 WordPress 深度整合，並特別針對台灣市場最普及的通訊軟體 LINE，教你打造自動化的訊息推播、互動式客服與行銷流程。你將不再僅限於網站內部的操作，而是能將網站數據與外部服務串聯，創造出更具智慧與互動性的商業應用。

準備好解放你的工作流，讓網站成為更聰明的自動化中心了嗎？讓我們開始這趟讓工作事半功倍的旅程吧！

---

## 課程目標

這門課的核心目標是讓你掌握「n8n 自動化流程設計」與「WordPress 服務串接」的能力。完成本課程後，你將能夠：

*   **獨立部署與管理 n8n：** 理解 n8n 的運作原理，並能在自己的環境中建置與維護 n8n 服務。
*   **精通 n8n 與 WordPress 整合：** 
    *   熟練使用 n8n 的 **WordPress / WooCommerce 專用節點**。
    *   運用 **HTTP Request 節點直接與 WordPress REST API v2 互動**，實現更彈性與深度的資料讀寫。
    *   利用 WordPress Webhooks，讓網站事件精準觸發 n8n 工作流。
*   **深入應用 LINE Messaging API：** 掌握 LINE Developers 平台設定，並透過 **強化版的 n8n LINE Messaging 節點 (參考：`elct9620/n8n-nodes-line-messaging`)**，發送多種 LINE 訊息，**精通 Flex Message 設計**，並打造豐富的互動體驗。
*   **設計商業級自動化情境：** 結合 WordPress 內容、WooCommerce 訂單、表單提交與 LINE，實作新文章通知、訂單提醒、**Google Sheets 同步**、顧客關懷等多元應用。
*   **掌握 n8n 進階技巧：** 學會使用**模組化工作流**與 **Code 節點**處理複雜邏輯，並建立穩健的錯誤處理機制。

---

## 課程單元總覽

這 30 小時的課程將分為以下幾個主要單元：

### 01. n8n 基礎與核心操作

本單元將介紹 n8n 的基本概念、運作模式，以及如何建置您的 n8n 工作環境，並熟悉核心節點的操作。

*   01.01 課程介紹：n8n 與 WordPress 自動化協作的價值
*   01.02 n8n 核心概念與應用場景 (workflow, node, trigger, action)
*   01.03 n8n 環境建置 (Cloud / Local Docker)
*   01.04 (實務) n8n 核心節點操作 (Set, Merge, IF, Code) 與資料結構處理

### 02. n8n 與 WordPress 核心整合

本單元將深入探討 n8n 如何透過 WordPress REST API 進行資料互動，並利用 Webhooks 實現 WordPress 事件的自動化觸發。我們將涵蓋使用 n8n 專用節點以及直接透過 HTTP Request 節點與 REST API v2 溝通的技巧。

*   02.01 WordPress REST API 深度解析 (含 v2 API 與驗證機制：應用程式密碼)
*   02.02 (實作) 使用 n8n 專用節點讀寫 WordPress/WooCommerce 資料
*   02.03 (實作) 使用 HTTP Request 節點讀取 WP 資料 (GET, 複雜查詢)
*   02.04 (實作) 使用 HTTP Request 節點寫入 WP 資料 (POST/PUT, 更新文章/ACF)
*   02.05 (實務) WordPress Webhooks 介紹：如何讓 WP 事件觸發 n8n 工作流

### 03. LINE Messaging API 深度應用

本單元將專注於台灣最受歡迎的通訊軟體 LINE。您將學習如何設定 LINE Developers 帳號，並透過 `n8n-nodes-line-messaging` 強化版的 LINE Messaging 節點，發送多種訊息類型，甚至建立互動式圖文選單。

*   03.01 LINE Developers 帳號設定與 Messaging API 啟用
*   03.02 (實作) 運用 `n8n-nodes-line-messaging` 節點：發送文字、圖片、貼圖訊息
*   03.03 (實作) LINE Flex Message 深度實戰 (含 LINE Flex Message Simulator)
*   03.04 (實作) LINE 其他訊息類型 (Quick Reply, Imagemap, Template Messages)
*   03.05 (實作) 建立 LINE Rich Menu (圖文選單) 並透過 n8n 管理
*   03.06 (實務) LINE Webhooks：接收使用者訊息與事件 (打造互動式 LINE Bot)

### 04. n8n 與 LINE & WordPress 商業情境整合

將前面學到的知識融會貫通，在本單元中，您將實作多個基於真實商業情境的自動化工作流，提升網站的互動性與營運效率。

*   04.01 (實作) WordPress 新文章發布，自動推播 LINE Flex Message
*   04.02 (實作) WooCommerce 新訂單通知 LINE 客服並同步記錄到 Google Sheets
*   04.03 (實作) 處理 WordPress 表單 (如 WPForms) 提交，自動回覆 LINE 訊息
*   04.04 (實作) 結合 FluentCRM：特定顧客行為 (例如：購買高單價商品) 後 LINE 自動化關懷
*   04.05 (實作) 打造 LINE 互動式客服：使用者輸入關鍵字查詢 WordPress 文章或 WooCommerce 訂單狀態

### 05. 進階應用與部署策略

本單元將探討 n8n 工作流的穩定性、模組化、錯誤處理與部署策略，確保您的自動化系統能夠穩健且高效地運行。

*   05.01 n8n 進階技巧：模組化工作流 (Execute Workflow)
*   05.02 n8n 進階技巧：Code 節點的 JavaScript 應用 (資料處理與邏輯判斷)
*   05.03 n8n 錯誤處理 (Error Workflow) 與日誌監控
*   05.04 n8n 部署與維護策略 (Docker Compose, PM2, 版本更新)

---

## 學習前的準備

這是一門進階課程，我們假設你已經具備以下基礎：

*   熟悉 WordPress 後台操作 (已完成 MoksaWP 課程一)。
*   對 WordPress REST API 有基本認識 (已完成 MoksaWP 課程三)。
*   具備基本的程式邏輯概念，了解 API 串接運作方式。
*   擁有 LINE Developers 帳號 (課程中會引導建立)。

準備好了嗎？這將是你釋放 WordPress 潛力、打造智慧自動化網站的關鍵一步！

讓我們開始這趟讓工作事半功倍的旅程吧！

---

## 附錄

*   **附錄 A：n8n 常用節點參考**
*   **附錄 B：LINE Messaging API 與 `n8n-nodes-line-messaging` 參考**
    *   LINE Messaging API 官方文件
    *   `n8n-nodes-line-messaging` GitHub 專案：`https://github.com/elct9620/n8n-nodes-line-messaging`
