# 虛擬貨幣投資幣種管理系統

本系統旨在幫助使用者管理加密貨幣投資組合，提供交易紀錄、資產統計分析，並支援持有幣種的管理功能。

---

## 成員自我介紹

您好！我們是虎尾科技大學四資工三乙的學生，以下是我們專題的成員自我介紹：

* **組長**：王忠仁（boxcat-none）
  **學號**：41143209
  **興趣**：觀看 YouTube 的旅遊、美食影片，並從中學習各種知識。

* **組員**：張家誠（Adsgfjhk）
  **學號**：41143231
  **興趣**：閱讀科技與程式設計文章、手遊與打球放鬆。

* **組員**：劉向宏（liuleo0518）
  **學號**：41143248
  **興趣**：打網球（體育績優升學）、現專注於資訊工程。

---

## 功能特色

* **使用者管理**：帳號註冊、登入、權限設定
* **資產管理**：查看持有幣種、實時價格、盈虧計算
* **交易紀錄**：記錄買入、賣出、交易時間與價格

---

## 系統需求

### 功能性需求

#### 使用者管理：

* 使用者可以註冊帳號，提供使用者名稱、電子郵件和密碼。
* 使用者可以通過電子郵件和密碼登入系統。
* 系統應支援權限設定，區分一般使用者與管理員角色。
* 使用者可以更新個人資料（例如電子郵件或密碼）。

#### 資產管理：

* 使用者可以查看當前持有的所有幣種及其數量。
* 系統應計算每種幣種的盈虧（基於買入價格與當前價格）。
* 使用者可以新增或移除持有的幣種。

#### 交易紀錄：

* 使用者可以記錄買入和賣出的交易，包括幣種、數量、價格和交易時間。
* 系統應提供交易歷史查詢功能，按時間或幣種過濾。
* 交易紀錄應自動更新持有幣種的數量（例如賣出後減少持有量）。

### 非功能性需求

#### 效能：

* 系統應快速完成一般查詢。
* 系統應支持多名使用者同時操作，且無顯著延遲。

#### 安全性：

* 使用者密碼必須加密儲存。
* 系統應防止常見的安全漏洞。

#### 可用性：

* 系統介面應直觀，支援桌上型和行動裝置瀏覽。
* 提供錯誤訊息提示。

#### 可維護性：

* 資料庫結構應設計為易於擴展。
* 程式碼應遵循模組化設計，方便後續維護和更新。

#### 可靠性：

* 系統應保證資料一致性。

---

## 資料庫結構

### 1. 使用者表（users）

| 欄位名稱           | 類型      | 描述         |
| -------------- | ------- | ---------- |
| id             | INT     | 使用者 ID（主鍵） |
| username       | VARCHAR | 使用者名稱      |
| password\_hash | VARCHAR | 密碼（加密）     |
| email          | VARCHAR | 電子郵件       |

### 完整性限制說明

**id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），自動遞增（AUTO_INCREMENT）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 -2,147,483,648 到 2,147,483,647
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**username**：
- 約束：非空（NOT NULL）
- 是否可重複：允許重複
- 長度限制：VARCHAR(50)，最多 50 個字符
- 特殊符號限制：支援字母、數字、下劃線、連字符
- 資料型態：VARCHAR(50)，可變長度字串

**password_hash**：
- 約束：非空（NOT NULL）
- 是否可重複：允許重複
- 長度限制：VARCHAR(255)，最多 255 個字符
- 特殊符號限制：支援所有字符
- 資料型態：VARCHAR(255)，可變長度字串

**email**：
- 約束：非空（NOT NULL），唯一（UNIQUE）
- 是否可重複：不可重複
- 長度限制：VARCHAR(100)，最多 100 個字符
- 特殊符號限制：支援字母、數字、點、連字符、下劃線、@
- 資料型態：VARCHAR(100)，可變長度字串

### 舉例

```
id | username       | password_hash         | email
---+---------------+-----------------------+-------------------------
1  | john_doe      | hashed_password_123   | john@example.com
2  | jane_smith    | hashed_password_456   | jane@example.com
3  | alex_wong     | hashed_password_789   | alex.wong@example.com
4  | emily_chen    | hashed_password_101   | emily.chen@example.com
5  | michael_lee   | hashed_password_202   | michael.lee@example.com
6  | sarah_kim     | hashed_password_303   | sarah.kim@example.com
7  | david_park    | hashed_password_404   | david.park@example.com
8  | laura_wu      | hashed_password_505   | laura.wu@example.com
9  | chris_tan     | hashed_password_606   | chris.tan@example.com
10 | sophia_liu    | hashed_password_707   | sophia.liu@example.com
```


### 2. 幣種表（cryptos）

| 欄位名稱           | 類型      | 描述            |
| -------------- | ------- | ------------- |
| id             | INT     | 幣種 ID（主鍵）     |
| symbol         | VARCHAR | 幣種代號（BTC、ETH） |
| name           | VARCHAR | 幣種名稱          |
| current\_price | DECIMAL | 當前價格          |

### 完整性限制說明

**id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），自動遞增（AUTO_INCREMENT）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 -2,147,483,648 到 2,147,483,647
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**symbol**：
- 約束：非空（NOT NULL），唯一（UNIQUE）
- 是否可重複：不可重複
- 長度限制：VARCHAR(10)，最多 10 個字符
- 特殊符號限制：僅限大寫字母、數字
- 資料型態：VARCHAR(10)，可變長度字串

**name**：
- 約束：非空（NOT NULL）
- 是否可重複：允許重複
- 長度限制：VARCHAR(50)，最多 50 個字符
- 特殊符號限制：支援字母、數字、空格、連字符
- 資料型態：VARCHAR(50)，可變長度字串

**current_price**：
- 約束：非空（NOT NULL）
- 是否可重複：允許重複
- 長度限制：DECIMAL(15, 2)，總長 15 位，含 2 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(15, 2)，固定精度十進位數

### 舉例

```
id | symbol | name            | current_price
---+--------+-----------------+---------------
1  | BTC    | Bitcoin         | 60000.50
2  | ETH    | Ethereum        | 3000.25
3  | BNB    | Binance Coin    | 600.75
4  | ADA    | Cardano         | 1.85
5  | XRP    | Ripple          | 0.95
6  | SOL    | Solana          | 150.30
7  | DOT    | Polkadot        | 20.45
8  | DOGE   | Dogecoin        | 0.35
9  | MATIC  | Polygon         | 1.20
10 | LINK   | Chainlink       | 25.60
```

### 3. 持倉表（holdings）

| 欄位名稱       | 類型      | 描述         |
| ---------- | ------- | ---------- |
| id         | INT     | 持倉 ID（主鍵）  |
| user\_id   | INT     | 使用者 ID（外鍵） |
| crypto\_id | INT     | 幣種 ID（外鍵）  |
| amount     | DECIMAL | 持有數量       |
| buy\_price | DECIMAL | 買入價格       |

### 完整性限制說明

**id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），自動遞增（AUTO_INCREMENT）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 0 到 2,147,483,647，從1開始
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**user_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES users(id)）
- 是否可重複：允許重複
- 長度限制：INT，與 users.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**crypto_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES cryptos(id)）
- 是否可重複：允許重複
- 長度限制：INT，與 cryptos.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**amount**：
- 約束：非空（NOT NULL），CHECK (amount >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(15, 8)，總長 15 位，含 8 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(15, 8)，固定精度十進位數

**buy_price**：
- 約束：非空（NOT NULL），CHECK (buy_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(15, 2)，總長 15 位，含 2 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(15, 2)，固定精度十進位數

### 舉例

```
id | user_id | crypto_id | amount       | buy_price
---+---------+-----------+--------------+-----------
1  | 1       | 1         | 0.50000000   | 58000.00
2  | 2       | 2         | 10.00000000  | 2900.00
3  | 3       | 3         | 15.00000000  | 590.00
4  | 4       | 4         | 1000.00000000| 1.70
5  | 5       | 5         | 5000.00000000| 0.90
6  | 6       | 6         | 20.00000000  | 140.00
7  | 7       | 7         | 50.00000000  | 19.50
8  | 8       | 8         | 10000.00000000| 0.30
9  | 9       | 9         | 800.00000000 | 1.10
10 | 10      | 10        | 40.00000000  | 24.00
```

### 4. 交易紀錄表（transactions）

| 欄位名稱              | 類型        | 描述         |
| ----------------- | --------- | ---------- |
| id                | INT       | 交易 ID（主鍵）  |
| user\_id          | INT       | 使用者 ID（外鍵） |
| crypto\_id        | INT       | 幣種 ID（外鍵）  |
| transaction\_type | VARCHAR   | 交易類型（買/賣）  |
| amount            | DECIMAL   | 交易數量       |
| price             | DECIMAL   | 交易價格       |
| timestamp         | TIMESTAMP | 交易時間       |

### 完整性限制說明

**id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），自動遞增（AUTO_INCREMENT）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 -2,147,483,648 到 2,147,483,647
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**user_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES users(id)）
- 是否可重複：允許重複
- 長度限制：INT，與 users.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**crypto_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES cryptos(id)）
- 是否可重複：允許重複
- 長度限制：INT，與 cryptos.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**transaction_type**：
- 約束：非空（NOT NULL），CHECK (transaction_type IN ('buy', 'sell'))
- 是否可重複：允許重複
- 長度限制：VARCHAR(10)，最多 10 個字符
- 特殊符號限制：僅限 "buy" 或 "sell"
- 資料型態：VARCHAR(10)，可變長度字串

**amount**：
- 約束：非空（NOT NULL），CHECK (amount > 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(15, 8)，總長 15 位，含 8 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(15, 8)，固定精度十進位數

**price**：
- 約束：非空（NOT NULL），CHECK (price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(15, 2)，總長 15 位，含 2 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(15, 2)，固定精度十進位數

**timestamp**：
- 約束：非空（NOT NULL），DEFAULT CURRENT_TIMESTAMP
- 是否可重複：允許重複
- 長度限制：TIMESTAMP，範圍 1970-01-01 00:00:01 到 2038-01-19 03:14:07 UTC
- 特殊符號限制：格式 YYYY-MM-DD HH:MM:SS，僅限數字、連字符、冒號、空格
- 資料型態：TIMESTAMP，時間戳型態，儲存日期和時間

### 舉例

```
id | username      | symbol | transaction_type | amount       | price    | timestamp
---+---------------+--------+------------------+--------------+----------+-------------------------
1  | john_doe      | BTC    | buy              | 0.50000000   | 58000.00 | 2025-05-01 10:00:00
2  | jane_smith    | ETH    | buy              | 10.00000000  | 2900.00  | 2025-05-02 12:00:00
3  | alex_wong     | BNB    | buy              | 15.00000000  | 590.00   | 2025-05-03 14:30:00
4  | emily_chen    | ADA    | buy              | 1000.00000000| 1.70     | 2025-05-04 09:15:00
5  | michael_lee   | XRP    | buy              | 5000.00000000| 0.90     | 2025-05-05 11:45:00
6  | sarah_kim     | SOL    | buy              | 20.00000000  | 140.00   | 2025-05-06 16:20:00
7  | david_park    | DOT    | sell             | 25.00000000  | 21.00    | 2025-05-07 08:00:00
8  | laura_wu      | DOGE   | buy              | 10000.00000000| 0.30    | 2025-05-08 13:10:00
9  | chris_tan     | MATIC  | sell             | 400.00000000 | 1.25     | 2025-05-09 15:25:00
10 | sophia_liu    | LINK   | buy              | 40.00000000  | 24.00    | 2025-05-10 17:50:00
```
---

## ER Diagram

![ER Diagram](./ER_Diagram.png)

## 資料庫Schema(SQL)

### 1. 創建資料表

```sql
-- 使用者表
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE
);

-- 幣種表
CREATE TABLE cryptos (
    id INT PRIMARY KEY,
    symbol VARCHAR(10) NOT NULL UNIQUE,
    name VARCHAR(50) NOT NULL,
    current_price DECIMAL(15, 2) NOT NULL
);

-- 持倉表
CREATE TABLE holdings (
    id INT PRIMARY KEY,
    user_id INT NOT NULL,
    crypto_id INT NOT NULL,
    amount DECIMAL(15, 8) NOT NULL,
    buy_price DECIMAL(15, 2) NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (crypto_id) REFERENCES cryptos(id)
);

-- 交易紀錄表
CREATE TABLE transactions (
    id INT PRIMARY KEY,
    user_id INT NOT NULL,
    crypto_id INT NOT NULL,
    transaction_type VARCHAR(10) NOT NULL CHECK (transaction_type IN ('buy', 'sell')),
    amount DECIMAL(15, 8) NOT NULL,
    price DECIMAL(15, 2) NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (crypto_id) REFERENCES cryptos(id)
);
```

## 團隊分工

* **組長**：王忠仁（boxcat-none）
  **工作內容**：自我介紹、功能特色、系統需求、資料庫結構、完整性限制說明、舉例、資料庫Schema(SQL)

* **組員**：張家誠（Adsgfjhk）
  **工作內容**：自我介紹、ER Diagram、功能特色、系統需求

* **組員**：劉向宏（liuleo0518）
  **工作內容**：自我介紹、資料庫結構、舉例、完整性限制說明
---

