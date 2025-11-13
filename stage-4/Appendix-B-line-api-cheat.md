# 附錄 B：LINE Messaging API 與 n8n-nodes-line-messaging 參考

嗨，歡迎來到 n8n 與 WordPress 協作的進階附錄章節。在前面的課程中，我們可能已經使用像 OrderChatz 或 Order Notify 這類方便的工具來串接 LINE 通知。然而，作為一位專業的開發者或網站管理者，直接了解其背後的運作原理——LINE Messaging API，並學會如何透過 n8n 這類自動化工具與之互動，將為你開啟無限的可能性。

本附錄的目標是提供一份清晰的參考指南，讓你快速掌握 LINE Messaging API 的核心觀念，以及如何在 n8n 中使用 `n8n-nodes-line-messaging` 這個強大的社群節點。

---

## 1. 核心觀念：認識 LINE Messaging API

在開始實作之前，有幾個來自 LINE 官方的**核心觀念**你必須先理解。

### 1.1 LINE Provider 與 Channel

*   **Provider (提供者):** 就像是你的公司或品牌。一個 Provider 底下可以擁有多個不同的 Channel。
*   **Channel (頻道):** 這就是你的 LINE 官方帳號 (LINE OA) 的本體。每個 Channel 都有自己獨立的設定、權限和 API 金鑰。我們在 n8n 中操作的對象，就是這個 **Channel**。

你可以在 [LINE Developers Console](https://developers.line.biz/console/) 中管理你的 Providers 和 Channels。

``
*截圖說明：LINE Developers Console 中顯示 Provider 與其下的 Channel。*

### 1.2 Channel Access Token (通道權杖)

這是與你的 LINE Channel 溝通的**最重要的金鑰**。任何對 Messaging API 的請求 (Request)，都必須包含這個 Token 來驗證你的身份。

*   **如何取得：**
    1.  登入 LINE Developers Console。
    2.  選擇你的 Provider > 選擇你的 Channel。
    3.  切換到「**Messaging API**」分頁。
    4.  滑到最下方，你會看到「**Channel access token**」。點擊「**Issue**」按鈕即可產生一組長效型的權杖。

*   **Moksa 技巧：** 這組 Token **極度機密**，絕對不要外洩，等同於你 LINE 官方帳號的密碼。在 n8n 中，我們一定會將它儲存在 **Credentials (憑證)** 裡，而不是直接寫在工作流的節點中。

``
*截圖說明：在 Messaging API 分頁中找到 Channel access token 的位置。*

### 1.3 使用者 ID (User ID)

每個將你的官方帳號加為好友的 LINE 用戶，都會被分配一組獨一無二的 **User ID** (格式通常是 `U` 開頭的一長串字元)。這個 ID 是你**主動**傳送訊息給特定用戶的唯一識別碼。

*   **重要觀念：** 你**無法**透過 LINE API 直接取得一個用戶的 LINE ID (他們在 App 中設定的那個)。你只能取得這個由 LINE 系統產生的 `User ID`。
*   **如何取得：** 當用戶傳送訊息給你、或觸發你設定的 Webhook 事件 (例如：加入好友) 時，LINE 會將包含 `User ID` 的資料包 (Payload) 傳送到你的 Webhook URL。這也是 n8n 的 LINE Trigger 節點能接收到用戶身份的原理。

### 1.4 Reply Token vs. Push Message (回覆 vs. 推播)

這是新手最容易混淆的觀念，但至關重要。

*   **Reply Message (回覆訊息):**
    *   **觸發時機：** 僅當用戶**主動**傳送訊息給你時，你才能「回覆」他。
    *   **必要條件：** 你必須使用該次互動產生的一組**有時效性**的 `replyToken`。
    *   **時效性：** `replyToken` 非常短暫 (約 30 秒)，用過一次或過期後即失效。
    *   **費用：** 免費。
    *   **n8n 節點：** `LINE` > `Operation: Reply Message`。

*   **Push Message (推播訊息):**
    *   **觸發時機：** **任何時候**，只要你高興，你都可以「主動推播」訊息給已加你好友的用戶。
    *   **必要條件：** 你必須知道對方的 `User ID`。
    *   **時效性：** 無。
    *   **費用：** **需要付費** (根據你的 LINE 官方帳號方案而定)。
    *   **n8n 節點：** `LINE` > `Operation: Push Message`。

**Moksa 技巧：** 電商網站的「訂單成立通知」、「出貨通知」等，都屬於**主動推播**，因此都是 **Push Message**。這也是為什麼像 OrderChatz 這類外掛需要一個機制來讓用戶「綁定」他們的 LINE 帳號，其目的就是為了取得並儲存客戶的 `User ID`，以便在未來觸發事件時可以主動推播訊息。

### 1.5 訊息物件 (Message Objects)

你能傳送的訊息不只是文字。LINE API 支援多種格式，常見的有：

*   **Text:** 純文字訊息。
*   **Sticker:** 貼圖。
*   **Image:** 圖片。
*   **Video:** 影片。
*   **Template Messages:** 預設版型的訊息，例如「按鈕樣板 (Buttons Template)」、「確認樣板 (Confirm Template)」。
*   **Flex Messages:** **功能最強大、彈性最高**的訊息格式。你可以用類似 HTML/CSS 的 JSON 結構來打造非常豐富的卡片式訊息。WooCommerce 的訂單摘要、產品推薦等，都非常適合用 Flex Message 呈現。

---

## 2. `n8n-nodes-line-messaging` 節點詳解

這個由社群開發的節點 (`n8n-nodes-line-messaging`) 極大地簡化了我們在 n8n 中與 LINE Messaging API 的互動。

### 2.1 安裝社群節點

**步驟 1：** 在 n8n 的主畫面上，點擊左側的「Settings」。
**步驟 2：** 選擇「Community Nodes」。
**步驟 3：** 點擊「Install a community node」。
**步驟 4：** 在 **NPM Package Name** 欄位中，輸入 `n8n-nodes-line-messaging`，然後點擊「Install」。
**步驟 5：** 安裝成功後，n8n 會提示需要重啟服務。重啟後即可在節點面板中搜尋到「LINE」節點。

``
*截圖說明：在 n8n 中安裝社群節點的畫面。*

### 2.2 建立憑證 (Credentials)

**步驟 1：** 在 n8n 主畫面的左側選單，點擊「Credentials」。
**步驟 2：** 點擊右上角的「Add Credential」按鈕。
**步驟 3：** 在搜尋框中輸入「LINE」，找到「LINE Messaging API」並點擊它。
**步驟 4：**
*   **Credential Name:** 給這個憑證一個好辨識的名稱，例如 `Moksa Demo LINE OA`。
*   **Channel Access Token:** 將你從 LINE Developers Console 取得的**通道權杖**完整貼上。

**步驟 5：** 點擊「Save」。這樣你的金鑰就安全地儲存好了。

### 2.3 常用節點操作

這個節點同時包含「觸發 (Trigger)」和「操作 (Operation)」兩種功能。

#### **LINE (Trigger)**

這是用來**接收**從 LINE 平台傳來的事件的進入點。

*   **原理：** 它會在你的 n8n 工作流中產生一個獨一無二的 Webhook URL。你需要將這個 URL 貼到 LINE Developers Console 的 `Messaging API > Webhook settings > Webhook URL` 欄位中。
*   **用途：** 當用戶傳訊息、加好友、封鎖帳號時，LINE 就會把事件資料（包含 `userId`, `replyToken` 等）傳送到這個 URL，進而觸發你的 n8n 工作流。

``
*截圖說明：LINE Trigger 節點產生的 Webhook URL 以及 LINE Developer後台貼上 URL 的位置。*

#### **LINE (Operation: Push Message)**

這是最常用的**主動推播**操作。

*   **必填欄位：**
    *   **`To`:** 接收訊息的目標 **User ID**。可以填寫單一 ID，也可以傳入一個包含多個 ID 的陣列。
    *   **`Messages`:** 選擇「Add Message Item」，然後選擇你想傳送的訊息類型 (Text, Sticker, Flex, etc.)。
*   **資料來源：** `To` 欄位的 User ID 通常來自前面的節點，例如從資料庫 (WordPress `usermeta` 表) 撈取，或是從 CRM (如 FluentCRM) 取得。

#### **LINE (Operation: Reply Message)**

用於**被動回覆**。

*   **必填欄位：**
    *   **`Reply Token`:** 這個 Token **必須**來自觸發此工作流的 LINE Trigger 節點。你通常會用 n8n 的表達式 (Expression) `{{ $json.replyToken }}` 來動態取得。
    *   **`Messages`:** 同 Push Message，設定你想要回覆的訊息內容。

---

## 3. 實務應用與參考資源

### 3.1 訊息設計：Flex Message Simulator

LINE 官方提供了一個視覺化的線上工具，讓你可以在不懂 JSON 的情況下，輕鬆「畫」出你想要的 Flex Message 卡片，並直接產生對應的 JSON 程式碼。

*   **工具網址：** [LINE Flex Message Simulator](https://developers.line.biz/flex-simulator/)
*   **Moksa 技巧：** 當你想在 n8n 的 LINE 節點中傳送 Flex Message 時，先用這個工具設計好，然後將產生的 JSON 完整複製，貼到節點的 `Flex Message (JSON)` 欄位即可。這是製作精美訂單通知、產品推薦卡片的不二法門。

``
*截圖說明：Flex Message Simulator 的操作介面，左邊是預覽，右邊是 JSON 程式碼。*

### 3.2 官方文件

當你需要查詢更進階的功能、API 的限制或錯誤代碼時，沒有比官方文件更準確的來源了。

*   **LINE Messaging API 官方文件:** [https://developers.line.biz/en/reference/messaging-api/](https://developers.line.biz/en/reference/messaging-api/)
*   **n8n-nodes-line-messaging 節點文件 (在 n8n.io 上):** [https://n8n.io/integrations/n8n-nodes-line-messaging/](https://n8n.io/integrations/n8n-nodes-line-messaging/)

希望這份附錄能幫助你更深入地理解 LINE Messaging API 與 n8n 之間的協作。當你掌握了這些基礎後，就能夠打造出遠超外掛限制、完全客製化的商業自動化流程。