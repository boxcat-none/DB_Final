# 虛擬貨幣投資幣種管理系統
本系統旨在幫助使用者管理加密貨幣投資組合，提供交易紀錄、資產統計分析，並支援持有幣種的管理功能。

## 成員自我介紹
您好！我們是虎尾科技大學四資工三乙的學生，以下是我們專題的成員自我介紹:
- 組長: 王忠仁([boxcat-none](https://github.com/boxcat-none))，學號: 41143209，興趣是在YouTube上觀看各種旅遊、美食的介紹影片，以及從影片中學習各種不同的知識。
- 組員: 張家誠([Adsgfjhk](https://github.com/Adsgfjhk))，學號: 41143231，我平時會去探索自己感興趣的事物，像是科技和程式設計方面的文章，這讓我能夠隨時了解最新的技術趨勢，平常也會玩手遊以及打球來讓我放鬆心情。
- 組員: 劉向宏([liuleo0518](https://github.com/liuleo0518))，學號: 41143248，我的興趣專長是打網球，從小就開始接觸這項運動，網球讓我可以更好的升學，升高中跟升大學都是體育績優考上的，現在這項運動變成我的休閒娛樂，我現在更著重於資訊工程。

## 功能特色
- **使用者管理**：帳號註冊、登入、權限設定  
- **資產管理**：查看持有幣種、實時價格、盈虧計算  
- **交易紀錄**：記錄買入、賣出、交易時間與價格 

## 資料庫結構
### 1. 使用者表（users）
<table>
    <tr>
        <th>欄位名稱</th>
        <th>類型</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>id</td>
        <td>INT</td>
        <td>使用者 ID（主鍵）</td>
    </tr>
    <tr>
        <td>username</td>
        <td>VARCHAR</td>
        <td>使用者名稱</td>
    </tr>
    <tr>
        <td>password_hash</td>
        <td>VARCHAR</td>
        <td>密碼（加密）</td>
    </tr>
    <tr>
        <td>email</td>
        <td>VARCHAR</td>
        <td>電子郵件</td>
    </tr>
</table>

### 2. 幣種表（cryptos）
<table>
    <tr>
        <th>欄位名稱</th>
        <th>類型</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>id</td>
        <td>INT</td>
        <td>幣種 ID（主鍵）</td>
    </tr>
    <tr>
        <td>symbol</td>
        <td>VARCHAR</td>
        <td>幣種代號（BTC、ETH）</td>
    </tr>
    <tr>
        <td>name</td>
        <td>VARCHAR</td>
        <td>幣種名稱</td>
    </tr>
    <tr>
        <td>current_price</td>
        <td>DECIMAL</td>
        <td>當前價格</td>
    </tr>
</table>

### 3. 持倉表（holdings）
<table>
    <tr>
        <th>欄位名稱</th>
        <th>類型</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>id</td>
        <td>INT</td>
        <td>持倉 ID（主鍵）</td>
    </tr>
    <tr>
        <td>user_id</td>
        <td>INT</td>
        <td>使用者 ID（外鍵）</td>
    </tr>
    <tr>
        <td>crypto_id</td>
        <td>INT</td>
        <td>幣種 ID（外鍵）</td>
    </tr>
    <tr>
        <td>amount</td>
        <td>DECIMAL</td>
        <td>持有數量</td>
    </tr>
    <tr>
        <td>buy_price</td>
        <td>DECIMAL</td>
        <td>買入價格</td>
    </tr>
</table>

### 4. 交易紀錄表（transactions）
<table>
    <tr>
        <th>欄位名稱</th>
        <th>類型</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>id</td>
        <td>INT</td>
        <td>交易 ID（主鍵）</td>
    </tr>
    <tr>
        <td>user_id</td>
        <td>INT</td>
        <td>使用者 ID（外鍵）</td>
    </tr>
    <tr>
        <td>crypto_id</td>
        <td>INT</td>
        <td>幣種 ID（外鍵）</td>
    </tr>
    <tr>
        <td>transaction_type</td>
        <td>VARCHAR</td>
        <td>交易類型（買/賣）</td>
    </tr>
    <tr>
        <td>amount</td>
        <td>DECIMAL</td>
        <td>交易數量</td>
    </tr>
    <tr>
        <td>price</td>
        <td>DECIMAL</td>
        <td>交易價格</td>
    </tr>
    <tr>
        <td>timestamp</td>
        <td>TIMESTAMP</td>
        <td>交易時間</td>
    </tr>
</table>
### ER Diagram
(https://github.com/boxcat-none/DB_Final/blob/main/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%202025-04-08%20172134.png)
