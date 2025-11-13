# 附錄 B：常用 Hooks (Action/Filter) 參考清單

嗨，歡迎來到 MoksaWP 開發課程的附錄章節！在 WordPress 與 WooCommerce 的世界裡，**Hooks (勾點)** 是你最好的朋友。它們是整個系統靈活、可擴展的核心。透過 Hooks，我們可以在不修改核心程式碼的前提下，安全地加入新功能或修改現有行為。

這個章節不是一個需要逐步操作的教學，而是一份**常用 Hooks 的參考清單**，我們將其分類整理，並提供基於 **Moksa 技術棧** 的實用範例。當你未來在開發專案時，可以隨時回來查閱，尋找靈感。

---

### 什麼是 Hooks？Action 與 Filter 的區別？

在開始之前，我們先快速複習一下最重要的觀念：

*   **Hooks (勾點):** 這是 WordPress 核心、佈景主題、外掛程式中預先定義好的「事件觸發點」。
*   **Action (動作):** 當某個事件發生時，用來「**執行某個動作**」。例如，「當使用者登入後，寄一封歡迎信」。Action 不會回傳任何值。我們使用 `add_action()` 來掛載函式。
*   **Filter (過濾器):** 當某個資料要被處理或輸出前，用來「**過濾或修改這個資料**」。例如，「在顯示文章標題前，在標題前面加上『最新消息：』」。Filter **必須**回傳修改後的值。我們使用 `add_filter()` 來掛載函式。

**Moksa 技巧：** 簡單記憶法 -> **Action 是「做事情」**，**Filter 是「改東西」**。

---

### 一、WordPress 核心常用 Hooks

這些是你在任何 WordPress 專案中，幾乎都會遇到的基礎 Hooks。

#### 1. `init` (Action)

*   **用途：** 在 WordPress 載入完畢，但還沒輸出任何畫面到瀏覽器前觸發。這是註冊 Custom Post Types (CPT)、Taxonomies 或處理 `$_GET`/`$_POST` 請求的最佳時機。
*   **範例：** 註冊一個名為「作品集 (Portfolio)」的 CPT。

    ```php
    add_action( 'init', 'moksa_register_portfolio_cpt' );
    function moksa_register_portfolio_cpt() {
        $args = [
            'public' => true,
            'label'  => '作品集',
            'supports' => ['title', 'editor', 'thumbnail'],
        ];
        register_post_type( 'portfolio', $args );
    }
    ```

#### 2. `wp_enqueue_scripts` (Action)

*   **用途：** 在網站前台正確地載入 CSS 樣式表與 JavaScript 檔案。這是**唯一推薦**的標準作法。
*   **範例：** 載入一個自訂的 `custom-style.css` 檔案。

    ```php
    add_action( 'wp_enqueue_scripts', 'moksa_enqueue_custom_styles' );
    function moksa_enqueue_custom_styles() {
        // 假設 CSS 檔案在子佈景主題的根目錄下
        wp_enqueue_style(
            'moksa-custom-style',
            get_stylesheet_directory_uri() . '/custom-style.css',
            [], // 依賴的樣式，例如 ['main-style']
            '1.0.0' // 版本號
        );
    }
    ```

#### 3. `the_content` (Filter)

*   **用途：** 過濾文章或頁面的主要內容。非常適合在內容前後自動加上資訊。
*   **範例：** 在每篇文章內容的結尾，加上一個版權宣告。

    ```php
    add_filter( 'the_content', 'moksa_add_copyright_notice' );
    function moksa_add_copyright_notice( $content ) {
        if ( is_single() && in_the_loop() && is_main_query() ) {
            $copyright_text = '<p><small>本文版權所有，轉載請註明出處。</small></p>';
            return $content . $copyright_text;
        }
        return $content;
    }
    ```

---

### 二、WooCommerce 常用 Hooks

WooCommerce 提供了極其豐富的 Hooks，讓我們可以客製化商店的每一個角落。

#### 1. 商品頁 (`single-product.php`)

*   **用途：** 調整單一商品頁面的佈局與內容。
*   **常見 Hooks (皆為 Action)：**
    *   `woocommerce_before_single_product_summary`：在商品主資訊區塊（包含圖片）之前。
    *   `woocommerce_single_product_summary`：在主資訊區塊內部，包含標題、價格、摘要、加入購物車按鈕等。
    *   `woocommerce_after_single_product_summary`：在商品主資訊區塊之後，通常是商品描述、評論等 Tab 區塊。
*   **範例：** 在「加入購物車」按鈕下方，新增一個「預計出貨天數」的提示。

    ````
    ```php
    // woocommerce_single_product_summary 內部有許多預設的 Action，
    // 例如 woocommerce_template_single_add_to_cart 的優先序是 30。
    // 我們可以掛載在它後面。
    add_action( 'woocommerce_single_product_summary', 'moksa_add_shipping_time_notice', 31 );
    function moksa_add_shipping_time_notice() {
        echo '<p class="shipping-notice"><small>付款完成後，預計 3-5 個工作天出貨。</small></p>';
    }
    ```

#### 2. 結帳頁 (`checkout`)

*   **用途：** 新增/修改結帳欄位、增加費用、或在訂單成立時執行特定動作。
*   **`woocommerce_checkout_fields` (Filter)**
    *   **用途：** 修改結帳頁面的所有欄位。
    *   **範例：** 將「公司名稱」欄位設為非必填。
        ```php
        add_filter( 'woocommerce_checkout_fields', 'moksa_make_company_name_optional' );
        function moksa_make_company_name_optional( $fields ) {
            // 將 billing (帳單) 分區中的 company 欄位的 required 屬性設為 false
            $fields['billing']['billing_company']['required'] = false;
            return $fields;
        }
        ```

*   **`woocommerce_cart_calculate_fees` (Action)**
    *   **用途：** 動態新增額外費用到購物車，例如：包裝費、急件處理費。
    *   **範例：** 當購物車總金額低於 500 元時，酌收 30 元處理費。
        ```php
        add_action( 'woocommerce_cart_calculate_fees', 'moksa_add_handling_fee' );
        function moksa_add_handling_fee( $cart ) {
            if ( is_admin() && ! defined( 'DOING_AJAX' ) ) return;

            if ( $cart->get_cart_contents_total() < 500 ) {
                $cart->add_fee( '處理費', 30 );
            }
        }
        ```

*   **`woocommerce_checkout_create_order` (Action)**
    *   **用途：** 在使用者點擊「下單購買」後，訂單物件已建立、但尚未存入資料庫前的瞬間。非常適合用來儲存自訂的結帳欄位資料。
    *   **範例：** 儲存一個名為 `custom_field` 的自訂欄位值到訂單 meta。
        ```php
        add_action('woocommerce_checkout_create_order', 'moksa_save_custom_field_to_order_meta', 10, 2);
        function moksa_save_custom_field_to_order_meta($order, $data) {
            if (isset($_POST['custom_field']) && !empty($_POST['custom_field'])) {
                $order->update_meta_data('_custom_field', sanitize_text_field($_POST['custom_field']));
            }
        }
        ```

#### 3. 訂單狀態變更

*   **`woocommerce_order_status_changed` (Action)**
    *   **用途：** 當訂單狀態改變時觸發，這是執行**自動化流程**的關鍵 Hook！例如：狀態變更為「已完成」時，自動將客戶加入 FluentCRM 的特定標籤。
    *   **範例：** 當訂單從任何狀態變為 `completed` (已完成) 時，執行某個動作。
        ```php
        add_action( 'woocommerce_order_status_changed', 'moksa_action_on_order_completed', 10, 4 );
        function moksa_action_on_order_completed( $order_id, $old_status, $new_status, $order ) {
            if ( 'completed' === $new_status ) {
                // 在這裡執行你的程式碼
                // 例如：呼叫外部 API、更新使用者角色、寄送客製化通知...
                // Moksa 技巧：整合 FluentCRM，將購買特定商品的客戶加上標籤
                if ( function_exists('fluentcrm_get_current_user') ) {
                    $contact = fluentcrm_get_current_user();
                    $tags_to_add = [123]; // 假設 123 是「VIP 客戶」標籤的 ID
                    $contact->attachTags($tags_to_add);
                }
            }
        }
        ```

---

### 三、Moksa 技術棧相關 Hooks

以下是一些針對我們推薦的外掛，非常實用的 Hooks 範例。

#### 1. RY Tools (物流)

*   **`ry_tools_shipping_method_label` (Filter)**
    *   **用途：** 客製化 RY Tools 在前台顯示的物流選項名稱。
    *   **範例：** 將「7-ELEVEN C2C」改為更友善的「7-11 超商取貨 (2-3 天到貨)」。
        ```php
        add_filter('ry_tools_shipping_method_label', 'moksa_customize_ry_shipping_label', 10, 2);
        function moksa_customize_ry_shipping_label($label, $method) {
            if ($method->get_method_id() === 'ry_c2c_shipping' && strpos($label, '7-ELEVEN') !== false) {
                return '7-11 超商取貨 (2-3 天到貨)';
            }
            return $label;
        }
        ```

#### 2. OrderChatz (LINE 客服與行銷)

*   **`orderchatz_line_message_text` (Filter)**
    *   **用途：** 在 OrderChatz 發送 LINE 通知前，動態修改訊息內容。
    *   **Moksa 技巧：** 這是一個超強大的行銷工具！你可以在出貨通知中，自動附上一組專屬的優惠券代碼，鼓勵客戶再次消費。
    *   **範例：** 在「已出貨」通知中，附上物流追蹤連結與感謝折扣碼。
        ```php
        // 假設你已經有一個函式 `moksa_generate_personal_coupon()` 可以為客戶產生專屬優惠券
        add_filter('orderchatz_line_message_text', 'moksa_enhance_shipped_notification', 10, 3);
        function moksa_enhance_shipped_notification($message, $order, $status) {
            if ($status === 'shipped') {
                // 取得物流追蹤碼 (假設你存在 order meta 中)
                $tracking_code = $order->get_meta('_shipping_tracking_code');
                $tracking_link = 'https://your-tracking-url.com?code=' . $tracking_code;

                // 產生專屬優惠券
                $coupon_code = moksa_generate_personal_coupon($order->get_customer_id());

                $new_message = "親愛的 {$order->get_billing_first_name()}，您的訂單 #{$order->get_id()} 已經出貨囉！\n";
                $new_message .= "物流追蹤碼：{$tracking_code}\n";
                $new_message .= "查詢連結：{$tracking_link}\n\n";
                $new_message .= "感謝您的支持！這是您下次購物專屬的 9 折優惠碼：{$coupon_code}";

                return $new_message;
            }
            return $message;
        }
        ```

#### 3. Rank Math SEO

*   **`rank_math/sitemap/entry` (Filter)**
    *   **用途：** 從 Rank Math 產生的 Sitemap 中，動態排除特定的文章或頁面。
    *   **範例：** 排除所有 CPT 為 `portfolio` (作品集) 且分類為 `drafts` (草稿) 的文章。
        ```php
        add_filter( 'rank_math/sitemap/entry', 'moksa_exclude_portfolio_drafts_from_sitemap', 10, 3 );
        function moksa_exclude_portfolio_drafts_from_sitemap( $url, $type, $post ) {
            if ( 'portfolio' === $post->post_type && has_term( 'drafts', 'portfolio_category', $post ) ) {
                return false; // 回傳 false 即可將其從 Sitemap 中排除
            }
            return $url;
        }
        ```

---

### 四、如何尋找與偵錯 Hooks？

清單永遠列不完，學會如何自己「找魚竿」更重要。

*   **Moksa 技巧：使用 Query Monitor 外掛**
    *   安裝並啟用 **Query Monitor** 外掛。
    *   在網站前台或後台，你會在上方管理列看到它的數據。
    *   點擊後，找到「Hooks & Actions」分頁。這裡會列出**當前頁面執行的所有 Action 和 Filter**，以及掛載在上面的函式與優先序。這是開發時最強大的偵錯與學習工具！
    ``

*   **直接閱讀原始碼**
    *   最直接的方法，就是打開外掛或佈景主題的 PHP 檔案。
    *   在程式碼中搜尋關鍵字 `do_action(` 或 `apply_filters(`。你就能找到所有可用的 Hooks，以及它們傳遞了哪些參數。

*   **官方文件**
    *   永遠不要忘記查閱官方文件，例如 [WooCommerce Hook Reference](https://woocommerce.github.io/code-reference/hooks/hooks.html) 就是你的好幫手。

希望這份清單能成為你開發路上的得力助手。記住，靈活運用 Hooks，是區分 WordPress 新手與專家的重要指標！