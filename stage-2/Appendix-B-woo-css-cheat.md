# 附錄 B：WooCommerce 常用 CSS Class/ID 速查

嗨，歡迎來到 MoksaWP 進階客製化課程的附錄章節。在品牌官網的設計過程中，我們時常需要微調 WooCommerce 的預設樣式，使其更符合我們的品牌視覺。例如，更改按鈕顏色、調整字體大小、或隱藏某些不需要的元素。

要做到這點，我們需要透過 CSS (Cascading Style Sheets) 來「選取」並「覆寫」這些元素的樣式。而 WooCommerce 為幾乎所有的頁面和元件都定義了非常語意化的 CSS Class (類別) 和 ID (識別碼)。

本章節就是一份為你整理好的「**速查表**」，讓你能夠快速找到常用頁面的關鍵 CSS Selectors (選取器)，加速你的客製化流程。

---

### 課前準備：如何找到任何元素的 CSS？

雖然我們提供了這份速查表，但**學會自己尋找 CSS 選取器是更重要的技能**。所有現代瀏覽器都內建了「開發者工具」，這就是你的武器。

**步驟 1：打開開發者工具**

*   在你想要修改的網頁元素上，點擊**滑鼠右鍵**。
*   在選單中選擇「**檢查**」(Inspect)。

``

**步驟 2：定位元素與樣式**

*   開發者工具會在畫面下方或右側打開。
*   左邊是 **HTML 結構**，你會看到你剛剛點擊的元素被反白標示。
*   右邊是 **CSS 樣式**，這裡會列出所有應用在該反白元素上的 CSS 規則。
*   你可以直接在右邊的樣式區塊中修改 CSS 數值，並**即時預覽**網頁上的變化。這個修改不會真的儲存，只是方便你測試。

``

**Moksa 技巧：** 學會使用開發者工具，你就不再需要死記硬背任何 Class 或 ID，而是能夠精準地對任何網站的任何元素進行樣式修改。

---

### 通用 & 全站性 Class

這些 Class 可能會出現在網站的多個地方。

*   `.woocommerce-message`：操作成功後的提示訊息 (例如：商品已加入購物車)。
*   `.woocommerce-error`：發生錯誤時的提示訊息 (例如：必填欄位未填寫)。
*   `.woocommerce-info`：一般資訊提示訊息 (例如：您有優惠券嗎？)。
*   `a.button`, `.button`：通用的按鈕樣式。
*   `.woocommerce-breadcrumb`：麵包屑導覽列。
*   `.woocommerce-result-count`：顯示「共 x 個商品中的 1–12 個」。
*   `.woocommerce-ordering`：商品排序的下拉選單。

---

### 商店頁 & 商品分類頁 (Shop / Archive)

這是陳列多個商品的主頁面。

*   `ul.products`：包覆所有商品的列表容器 (Grid 容器)。
*   `li.product`：單一商品項目的容器。
*   `li.product .woocommerce-loop-product__link`：包覆商品圖片和標題的連結。
*   `li.product .woocommerce-loop-product__title`：商品標題。
*   `li.product .price`：商品價格。
*   `li.product .add_to_cart_button`：商品列表上的「加入購物車」按鈕。
*   `.woocommerce-pagination`：底部的分頁導覽。

---

### 單一商品頁 (Single Product)

這是展示單一商品詳情的頁面。

*   `div.product`：整個單一商品內容的總容器。
*   `.woocommerce-product-gallery`：左側的商品圖片展示區塊。
*   `.summary.entry-summary`：右側的商品資訊總結區塊。
*   `.product_title.entry-title`：商品主標題。
*   `p.price`：商品價格。
*   `.woocommerce-product-details__short-description`：商品簡短描述。
*   `form.cart`：加入購物車的表單 (包含數量選擇和按鈕)。
*   `form.cart .quantity`：數量選擇器。
*   `form.cart .single_add_to_cart_button`：**主要的「加入購物車」按鈕**。
*   `.woocommerce-tabs`：下方的頁籤區塊 (說明、評論等)。
*   `.woocommerce-tabs ul.tabs`：頁籤的標題列。
*   `.woocommerce-Tabs-panel`：頁籤的內容區塊。
*   `.related.products`：相關商品區塊。

---

### 購物車頁 (Cart)

*   `.woocommerce-cart-form`：包覆整個購物車表格的表單。
*   `table.shop_table.cart`：購物車商品明細的表格。
*   `.product-remove`：移除商品按鈕。
*   `.product-thumbnail`：商品縮圖。
*   `.product-name`：商品名稱。
*   `.product-quantity`：商品數量選擇器。
*   `.actions .coupon`：優惠券輸入框和按鈕的容器。
*   `#coupon_code`：**優惠券代碼輸入框的 ID**。
*   `.cart-collaterals`：右側或下方的「購物車總計」區塊。
*   `.cart_totals`：購物車總計的詳細表格。
*   `.wc-proceed-to-checkout a.checkout-button`：**前往結帳的按鈕**。

---

### 結帳頁 (Checkout)

結帳頁的 Class 結構相對複雜，通常分為左右兩欄。

*   `form.woocommerce-checkout`：整個結帳頁面的表單。
*   `#customer_details`：左側顧客資訊欄位的容器。
*   `.woocommerce-billing-fields`：帳單地址欄位區塊。
*   `.woocommerce-shipping-fields`：運送地址欄位區塊。
*   `#order_review_heading`：右側「您的訂單」標題。
*   `#order_review`：右側訂單總覽的容器。
*   `table.shop_table.woocommerce-checkout-review-order-table`：訂單總覽的表格。
*   `#payment`：**付款方式區塊的 ID**。
*   `ul.wc_payment_methods`：付款方式選項列表 (綠界信用卡、ATM 等)。
*   `#place_order`：**「下單購買」按鈕的 ID**，這是最重要的按鈕之一。

---

### 我的帳號頁 (My Account)

*   `.woocommerce-account .woocommerce-MyAccount-navigation`：左側的導覽選單。
*   `.woocommerce-account .woocommerce-MyAccount-content`：右側的內容顯示區塊。

---

### 實戰範例：修改結帳頁「下單購買」按鈕的顏色

假設我們想把結帳頁的「下單購買」按鈕從預設顏色改成品牌主色 `#FF6600`。

**步驟 1：找到選取器**

根據上面的速查表，我們知道這個按鈕的 ID 是 `#place_order`。

**步驟 2：撰寫 CSS 規則**

我們要修改背景顏色 (background-color) 和文字顏色 (color)。

```css
/* 修改結帳頁下單購買按鈕樣式 */
#place_order {
    background-color: #FF6600 !important;
    color: #FFFFFF !important;
}

/* 修改滑鼠移上去時的按鈕樣式 */
#place_order:hover {
    background-color: #E65C00 !important; /* 滑鼠移上去時稍微變深 */
}
```

**Moksa 技巧：** 為什麼要加 `!important`？因為有些主題或頁面編輯器 (如 Elementor) 會用非常高權重的 CSS 規則來定義按鈕樣式。`!important` 可以強制覆寫這些規則。雖然不建議濫用，但在這種需要精準覆寫的場景下非常實用。

**步驟 3：貼上 CSS 程式碼**

*   前往 WordPress 後台 > **外觀 (Appearance)** > **自訂 (Customize)**。
*   點選「**附加的 CSS (Additional CSS)**」。
*   將上面這段程式碼貼進去。
*   點擊「**發佈 (Publish)**」。

``

現在，回到你的結帳頁面重新整理，就會看到按鈕顏色已經成功被修改了！

這份速查表是你未來進行網站視覺客製化時的最佳夥伴，建議你可以將它收藏起來，隨時查閱。