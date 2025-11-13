# 附錄 A：WP_Query 參數速查表

`WP_Query` 是 WordPress 的核心，它是一個極其強大且靈活的類別 (Class)，用於向 WordPress 資料庫請求並取得文章 (Posts)、頁面 (Pages) 或任何自訂文章類型 (Custom Post Types) 的資料。幾乎所有在 WordPress 前台看到的動態內容列表，都是透過 `WP_Query` 或其相關函式（如 `get_posts()`）來實現的。

對於佈景主題與外掛開發者來說，**精通 `WP_Query` 是區分新手與專家的關鍵**。本附錄將作為一份速查表，整理了最常用且最重要的參數，並提供符合 Moksa 開發實踐的範例。

---

### WP_Query 的基本結構

在深入了解各種參數之前，讓我們先回顧一個標準的 `WP_Query` 迴圈 (The Loop) 結構。這是你每次使用 `WP_Query` 時都會用到的樣板程式碼。

```php
<?php

// 1. 設定查詢參數陣列
$args = array(
    'post_type'      => 'post',        // 查詢文章類型為「文章」
    'posts_per_page' => 5,             // 每頁顯示 5 篇
    'orderby'        => 'date',        // 依照日期排序
    'order'          => 'DESC',        // 遞減排序 (最新的在前面)
);

// 2. 建立一個新的 WP_Query 實例
$the_query = new WP_Query( $args );

// 3. The Loop - 迴圈開始
if ( $the_query->have_posts() ) {
    while ( $the_query->have_posts() ) {
        $the_query->the_post(); // 設定全域 $post 物件，讓 a: the_title(), the_content() 等函式能運作

        // 在這裡放置你的 HTML 和範本標籤 (Template Tags)
        ?>
        <article id="post-<?php the_ID(); ?>">
            <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
            <div class="entry-content">
                <?php the_excerpt(); // 顯示摘要 ?>
            </div>
        </article>
        <?php
    }
} else {
    // 如果沒有找到任何文章，顯示此訊息
    echo '<p>抱歉，沒有找到符合條件的文章。</p>';
}

// 4. 重置 Post Data
// **Moksa 技巧：** 這是絕對必要的步驟！它會將全域 $post 物件還原到主查詢的狀態，
// 避免影響頁面其他部分的查詢結果（例如側邊欄、頁尾的小工具）。
wp_reset_postdata();

?>
```

---

### 常用參數分類速查

接下來，我們將參數按照功能進行分類，方便你快速查找。

#### 1. 文章與頁面參數 (Post & Page Parameters)

用於直接指定特定的文章或頁面。

| 參數 | 說明 | 範例 |
| :--- | :--- | :--- |
| `p` | 根據 **文章 ID** 取得單一文章。 | `'p' => 7` |
| `page_id` | 根據 **頁面 ID** 取得單一頁面。 | `'page_id' => 12` |
| `name` | 根據 **文章代稱 (Post Slug)** 取得單一文章。 | `'name' => 'hello-world'` |
| `pagename` | 根據 **頁面代稱 (Page Slug)** 取得單一頁面。 | `'pagename' => 'about-us'` |
| `post__in` | 傳入一個 **文章 ID 陣列**，只取得這些 ID 的文章。 | `'post__in' => array( 2, 15, 23 )` |
| `post__not_in` | 傳入一個 **文章 ID 陣列**，排除這些 ID 的文章。 | `'post__not_in' => array( 5, 10 )` |

#### 2. 文章類型與狀態參數 (Post Type & Status Parameters)

定義要查詢的內容類型和其狀態。

| 參數 | 說明 | 範例 |
| :--- | :--- | :--- |
| `post_type` | 指定文章類型。可以是 `'post'`, `'page'`, `'product'` (WooCommerce 商品) 或你用 CPT UI/ACF 建立的自訂文章類型。**此為最常用的參數之一**。可以傳入單一值或陣列。 | `'post_type' => 'product'`<br>`'post_type' => array( 'post', 'event' )` |
| `post_status` | 指定文章狀態。預設為 `'publish'`。其他常用值包含 `'draft'` (草稿), `'pending'` (待審), `'private'` (私密)。可以傳入單一值或陣列。 | `'post_status' => 'publish'`<br>`'post_status' => array( 'publish', 'private' )` |

#### 3. 排序與順序參數 (Order & Orderby Parameters)

控制查詢結果的排序方式。

| 參數 | 說明 | 範例 |
| :--- | :--- | :--- |
| `order` | 排序順序。`'ASC'` (遞增) 或 `'DESC'` (遞減)。預設為 `'DESC'`。 | `'order' => 'ASC'` |
| `orderby` | 排序依據的欄位。常用值：<br>- `'date'`: 發佈日期 (預設)<br>- `'title'`: 標題<br>- `'ID'`: 文章 ID<br>- `'comment_count'`: 留言數<br>- `'rand'`: 隨機排序<br>- `'meta_value'`: 依自訂欄位的值排序 (需搭配 `meta_key`)<br>- `'meta_value_num'`: 依自訂欄位的**數值**排序 (需搭配 `meta_key`) | `'orderby' => 'title'`<br>`'orderby' => 'meta_value_num'` |
| `meta_key` | 當 `orderby` 設為 `meta_value` 或 `meta_value_num` 時，**必須指定**要依據哪個自訂欄位來排序。 | `'meta_key' => 'product_price'` |

**範例：** 取得價格最高的 3 個 WooCommerce 商品。
```php
$args = array(
    'post_type'      => 'product',
    'posts_per_page' => 3,
    'meta_key'       => '_price', // WooCommerce 價格的 meta key
    'orderby'        => 'meta_value_num',
    'order'          => 'DESC',
);
```

#### 4. 分頁參數 (Pagination Parameters)

用於處理需要分頁的列表。

| 參數 | 說明 | 範例 |
| :--- | :--- | :--- |
| `posts_per_page` | 每頁顯示幾篇文章。設為 `-1` 表示顯示所有符合條件的文章 (**請謹慎使用，可能造成效能問題**)。 | `'posts_per_page' => 10` |
| `offset` | 略過前 N 篇文章。例如設為 `5`，查詢會從第 6 篇文章開始。**注意：使用 `offset` 會破壞 WordPress 的內建分頁功能。** | `'offset' => 5` |
| `paged` | 目前所在的頁碼。**這是實現標準分頁的正確方式**。通常會動態取得 URL 中的頁碼。 | `'paged' => get_query_var( 'paged' ) ? get_query_var( 'paged' ) : 1` |

#### 5. 分類法參數 (Taxonomy Parameters)

這是 `WP_Query` 最強大的功能之一，用於根據分類 (Category)、標籤 (Tag) 或自訂分類法 (Custom Taxonomy) 來篩選文章。

| 參數 | 說明 | 範例 |
| :--- | :--- | :--- |
| `cat` | 根據 **分類 ID** 取得文章。用負數表示排除。 | `'cat' => 5` (只取 ID=5)<br>`'cat' => -5` (排除 ID=5) |
| `category_name` | 根據 **分類代稱 (Slug)** 取得文章。 | `'category_name' => 'news'` |
| `tag` | 根據 **標籤代稱 (Slug)** 取得文章。 | `'tag' => 'featured'` |
| `tax_query` | **終極武器！** 用於複雜的分類法查詢。可以同時篩選多個分類法，並定義它們之間的邏輯關係 (`AND` 或 `OR`)。 | 見下方詳細範例 |

**`tax_query` 範例：**
假設我們要找所有 WooCommerce 商品，條件是：
1.  商品分類 (product_cat) 是「上衣」(tops) **或** 「褲子」(pants)
2.  **並且** 商品標籤 (product_tag) 是「特價」(sale)

```php
$args = array(
    'post_type' => 'product',
    'posts_per_page' => 12,
    'tax_query' => array(
        'relation' => 'AND', // 兩個條件之間是 AND 關係
        array(
            'taxonomy' => 'product_cat',    // 分類法：商品分類
            'field'    => 'slug',            // 用代稱來比對
            'terms'    => array( 'tops', 'pants' ), // 條件：上衣或褲子
            'operator' => 'IN',
        ),
        array(
            'taxonomy' => 'product_tag',    // 分類法：商品標籤
            'field'    => 'slug',            // 用代稱來比對
            'terms'    => 'sale',            // 條件：特價
        ),
    ),
);
```

#### 6. 自訂欄位參數 (Custom Field / Meta Parameters)

與 `tax_query` 同樣強大，用於根據 ACF 或其他外掛建立的自訂欄位值來篩選內容。

| 參數 | 說明 | 範例 |
| :--- | :--- | :--- |
| `meta_key` | 篩選出擁有特定 `meta_key` 的文章。 | `'meta_key' => 'event_date'` |
| `meta_value` | 篩選出 `meta_key` 的值等於此值的文章。必須與 `meta_key` 一起使用。 | `'meta_key' => 'event_city', 'meta_value' => 'Taipei'` |
| `meta_compare` | `meta_value` 的比較運算子。預設為 `'='`。其他值如 `'>'`, `'<'`, `'LIKE'`, `'NOT LIKE'`, `'IN'` 等。 | `'meta_compare' => '>='` |
| `meta_query` | **終極武器！** 用於複雜的自訂欄位查詢，結構與 `tax_query` 類似。 | 見下方詳細範例 |


**`meta_query` 範例：**
假設我們有一個自訂文章類型「活動 (event)」，並用 ACF 建立了兩個欄位：「活動日期 (event_date)」和「活動城市 (event_city)」。我們要找所有在「台北 (Taipei)」**而且**日期在「2024-01-01」之後的活動。

```php
$args = array(
    'post_type'  => 'event',
    'meta_query' => array(
        'relation' => 'AND', // 兩個條件之間是 AND 關係
        array(
            'key'     => 'event_city',
            'value'   => 'Taipei',
            'compare' => '=',
        ),
        array(
            'key'     => 'event_date',
            'value'   => '20240101', // ACF 日期選擇器通常儲存為 Ymd 格式
            'type'    => 'DATE',
            'compare' => '>=',
        ),
    ),
);
```

---

### **Moksa 技巧：** 使用 Query Monitor 進行除錯

在開發複雜的 `WP_Query` 時，你最好的朋友就是 **Query Monitor** 外掛。

1.  **步驟 1：安裝並啟用 Query Monitor**
    從 WordPress 後台安裝此外掛。啟用後，你會在頂部的管理員工具列看到一個新的數據面板。

2.  **步驟 2：執行你的程式碼**
    在你撰寫了 `WP_Query` 的頁面，重新整理前台。

3.  **步驟 3：檢查 Queries 面板**
    點擊管理員工具列上的 Query Monitor 面板，找到「Queries」分頁，再點選「Queries by Caller」。

    ``

4.  **步驟 4：找到你的查詢**
    在 Caller 列表中，找到你執行 `new WP_Query()` 的那個檔案與行數。點開它，你就可以看到：
    *   **完整的 SQL 語法：** WordPress 最終生成了什麼 SQL 語句來查詢資料庫。這是除錯的黃金資訊！
    *   **查詢時間：** 可以幫助你判斷這個查詢是否有效能問題。
    *   **影響的行數：** 查詢返回了多少筆資料。

透過分析 Query Monitor 提供的 SQL，你可以精準地判斷出是不是你的 `$args` 參數設定有誤，或是邏輯上有問題，這比盲目地 `var_dump()` 要有效率得多。

`WP_Query` 的世界博大精深，本速查表涵蓋了約 80% 的日常開發場景。當你需要更進階的功能時（例如巢狀查詢、地理資訊查詢等），請務必查閱官方的 [WordPress 開發者文件](https://developer.wordpress.org/reference/classes/wp_query/)。不斷練習與實驗，你很快就能夠駕馭這個強大的工具。