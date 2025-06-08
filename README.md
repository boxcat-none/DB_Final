# 虛擬貨幣投資幣種管理系統

## 目錄
- [1. 專案概述](#1-專案概述)
  - [1.1 系統簡介](#11-系統簡介)
  - [1.2 成員自我介紹](#12-成員自我介紹)
- [2. 功能與需求](#2-功能與需求)
  - [2.1 功能特色](#21-功能特色)
  - [2.2 使用者需求](#22-使用者需求)
  - [2.3 系統需求](#23-系統需求)
    - [使用者管理](#使用者管理)
    - [資產管理](#資產管理)
    - [交易紀錄](#交易紀錄)
  - [2.4 使用者案例](#24-使用者案例)
    - [一般使用者（User）](#一般使用者user)
    - [管理員（Admin）](#管理員admin)
    - [超級管理員（Super Admin）](#超級管理員super-admin)
- [3. ER Diagram](#3-er-diagram)
- [4. 資料庫結構](#4-資料庫結構)
  - [4.1 使用者表（users）](#41-使用者表users)
  - [4.2 使用者憑證表（user_credentials）](#42-使用者憑證表user_credentials)
  - [4.3 幣種表（cryptos）](#43-幣種表cryptos)
  - [4.4 歷史價格表（crypto_prices）](#44-歷史價格表crypto_prices)
  - [4.5 持倉表（holdings）](#45-持倉表holdings)
  - [4.6 交易紀錄表（transactions）](#46-交易紀錄表transactions)
- [5. 資料庫 Schema (SQL)](#5-資料庫-schema)
- [6. 視圖 (View)](#6-視圖-view)
  - [6.1 使用者管理](#61-使用者管理)
    - [使用者資料視圖（v_user_profile）](#使用者資料視圖v_user_profile)
  - [6.2 資產管理](#62-資產管理)
    - [(1) 持倉概覽視圖（v_user_holdings）](#1-持倉概覽視圖v_user_holdings)
    - [(2) 投資表現視圖（v_user_investment_performance）](#2-投資表現視圖v_user_investment_performance)
  - [6.3 交易紀錄](#63-交易紀錄)
    - [交易歷史視圖（v_user_transactions）](#交易歷史視圖v_user_transactions)
  - [6.4 市場資訊與分析](#64-市場資訊與分析)
    - [(1) 實時行情視圖（v_market_realtime）](#1-實時行情視圖v_market_realtime)
    - [(2) K 線圖視圖（v_kline_data）](#2-k-線圖視圖v_kline_data)
  - [6.5 視圖總覽與權限](#65-視圖總覽與權限)
- [7. 團隊分工](#7-團隊分工)
- [8. 報告連結](#8-報告連結)
- [9. 參考資料](#9-參考資料)

## 1. 專案概述

### 1.1 系統簡介
本系統為一虛擬貨幣投資管理平台，支援帳號管理、交易記錄、持倉追蹤與市場行情分析，幫助用戶高效管理投資組合。核心功能包括：
- 使用者管理：註冊、登入、權限分級。
- 交易紀錄：記錄買入/賣出交易。
- 資產管理：持倉檢視、盈虧計算、投資報告。
- 市場資訊：實時行情、K 線圖與技術指標。

### 1.2 成員自我介紹

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

## 2. 功能與需求

### 2.1 功能特色
- **使用者管理**：帳號註冊、登入、權限設定。
- **交易紀錄**：記錄買入、賣出、交易時間與價格。
- **資產管理**：查看持有幣種、實時價格、盈虧計算、分析報告。

### 2.2 使用者需求
- **註冊與登錄**：透過電子郵件與密碼註冊、登錄，支援密碼重置。
- **個人資料管理**：查看與更新 username、email。
- **交易記錄**：查看買入/賣出歷史。
- **持倉追蹤**：實時查看持倉數量、當前市值、平均買入價格、盈虧。
- **實時行情**：查看幣種價格、24小時漲跌幅。
- **歷史價格**：查看 K 線圖（1小時、4小時、日線），計算技術指標。
- **投資表現**：查看收益、投資分析報告。

### 2.3 系統需求
#### 使用者管理
- 使用者可註冊帳號，提供使用者名稱、電子郵件與密碼。
- 支援電子郵件與密碼登入，區分一般使用者、管理員與超級管理員。
- 使用者可更新個人資料。

#### 資產管理
- 使用者可查看持有的所有幣種及其數量。
- 系統計算每種幣種的盈虧。
- 支援新增或移除持有的幣種。
- 提供投資分析報告。

#### 交易紀錄
- 記錄買入與賣出交易，包含幣種、數量、價格與時間。
- 提供交易歷史查詢功能。

### 2.4 使用者案例
#### 一般使用者（User）
- 帳戶管理：註冊、更新資料、重置密碼。
- 投資組合管理：添加持倉、查看持倉與交易。
- 市場資訊：查看行情、歷史價格分析。

#### 管理員（Admin）
- 用戶管理：查看用戶、禁用帳戶。
- 幣種管理：上架或下架幣種。
- 包含一般使用者功能。

#### 超級管理員（Super Admin）
- 權限管理：創建管理員、修改權限。
- 系統配置：設定 API。
- 包含所有功能。

## 3. ER Diagram

![ER Diagram](./ER_Diagram.png)
## 4. 資料庫結構

### 4.1 使用者表（users）

| 欄位名稱     | 類型      | 描述         |
|--------------|-----------|--------------|
| id           | INT       | 使用者 ID（主鍵） |
| username     | VARCHAR   | 使用者名稱      |
| email        | VARCHAR   | 電子郵件       |
| role         | VARCHAR   | 使用者角色      |

#### 完整性限制說明

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

**email**：
- 約束：非空（NOT NULL），唯一（UNIQUE）
- 是否可重複：不可重複
- 長度限制：VARCHAR(100)，最多 100 個字符
- 特殊符號限制：支援字母、數字、點、連字符、下劃線、@
- 資料型態：VARCHAR(100)，可變長度字串

**role**：
- 約束：非空（NOT NULL），CHECK (role IN ('super_admin', 'admin', 'user'))
- 是否可重複：允許重複
- 長度限制：VARCHAR(20)，最多 20 個字符
- 特殊符號限制：僅限 'super_admin'、'admin'、'user'
- 資料型態：VARCHAR(20)，可變長度字串

#### 舉例

```
id | username      | email                   | role
---+---------------+-------------------------+------------
1  | john_doe      | john@example.com        | super_admin
2  | jane_smith    | jane@example.com        | admin
3  | alex_wong     | alex.wong@example.com   | admin
4  | emily_chen    | emily.chen@example.com  | user
5  | michael_lee   | michael.lee@example.com | user
6  | sarah_kim     | sarah.kim@example.com   | user
7  | david_park    | david.park@example.com  | user
8  | laura_wu      | laura.wu@example.com    | user
9  | chris_tan     | chris.tan@example.com   | user
10 | sophia_liu    | sophia.liu@example.com  | user
```

### 4.2 使用者憑證表（user_credentials）

| 欄位名稱       | 類型      | 描述         |
|----------------|-----------|--------------|
| user_id        | INT       | 使用者 ID（主鍵，外鍵） |
| password_hash  | VARCHAR   | 密碼（加密）     |

#### 完整性限制說明

**user_id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES users(id) ON DELETE CASCADE）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 -2,147,483,648 到 2,147,483,647
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**password_hash**：
- 約束：非空（NOT NULL）
- 是否可重複：允許重複
- 長度限制：VARCHAR(255)，最多 255 個字符
- 特殊符號限制：支援所有字符
- 資料型態：VARCHAR(255)，可變長度字串

#### 舉例

```
user_id | password_hash
--------+---------------------- 
1       | hashed_password_123
2       | hashed_password_456
3       | hashed_password_789
4       | hashed_password_101
5       | hashed_password_202
6       | hashed_password_303
7       | hashed_password_404
8       | hashed_password_505
9       | hashed_password_606
10      | hashed_password_707
```

### 4.3 幣種表（cryptos）

| 欄位名稱       | 類型      | 描述            |
|----------------|-----------|-----------------|
| id             | INT       | 幣種 ID（主鍵）     |
| symbol         | VARCHAR   | 幣種代號（BTC、ETH） |
| name           | VARCHAR   | 幣種名稱          |
| current_price  | DECIMAL   | 當前價格          |

#### 完整性限制說明

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
- 約束：非空（NOT NULL），CHECK (current_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

#### 舉例

```
id | symbol | name            | current_price
---+--------+-----------------+---------------
1  | BTC    | Bitcoin         | 60000.50000
2  | ETH    | Ethereum        | 3000.25000
3  | BNB    | Binance Coin    | 600.75000
4  | ADA    | Cardano         | 1.85000
5  | XRP    | Ripple          | 0.95000
6  | SOL    | Solana          | 150.30000
7  | DOT    | Polkadot        | 20.45000
8  | DOGE   | Dogecoin        | 0.35000
9  | MATIC  | Polygon         | 1.20000
10 | LINK   | Chainlink       | 25.60000
```
### 4.4 歷史價格表（crypto_prices）

| 欄位名稱      | 類型        | 描述              |
|---------------|-------------|-------------------|
| crypto_id     | INT         | 幣種 ID（外鍵）     |
| timestamp     | TIMESTAMP   | 價格記錄時間        |
| open_price    | DECIMAL     | 開盤價            |
| high_price    | DECIMAL     | 最高價            |
| low_price     | DECIMAL     | 最低價            |
| close_price   | DECIMAL     | 收盤價            |
| volume        | DECIMAL     | 交易量            |

#### 完整性限制說明

**crypto_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES cryptos(id) ON DELETE CASCADE），主鍵的一部分
- 是否可重複：與 timestamp 組合不可重複
- 長度限制：INT，32 位整數，範圍 -2,147,483,648 到 2,147,483,647
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**timestamp**：
- 約束：非空（NOT NULL），主鍵的一部分
- 是否可重複：與 crypto_id 組合不可重複
- 長度限制：TIMESTAMP，範圍 1970-01-01 00:00:01 到 2038-01-19 03:14:07 UTC
- 特殊符號限制：格式 YYYY-MM-DD HH:MM:SS，僅限數字、連字符、冒號、空格
- 資料型態：TIMESTAMP，時間戳型態，儲存日期和時間

**open_price**：
- 約束：非空（NOT NULL），CHECK (open_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

**high_price**：
- 約束：非空（NOT NULL），CHECK (high_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

**low_price**：
- 約束：非空（NOT NULL），CHECK (low_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

**close_price**：
- 約束：非空（NOT NULL），CHECK (close_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

**volume**：
- 約束：非空（NOT NULL），CHECK (volume >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(20, 10)，總長 20 位，含 10 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(20, 10)，固定精度十進位數

#### 舉例

```
crypto_id | timestamp            | open_price  | high_price  | low_price   | close_price | volume
----------+---------------------+-------------+-------------+-------------+-------------+----------------
1         | 2025-06-08 10:00:00 | 60000.50000 | 60250.75000 | 59800.25000 | 60120.30000 | 100.5000000000
1         | 2025-06-08 11:00:00 | 60120.30000 | 60300.00000 | 60050.10000 | 60280.45000 | 120.7500000000
2         | 2025-06-08 10:00:00 | 3000.25000  | 3050.50000  | 2980.75000  | 3020.15000  | 500.0000000000
2         | 2025-06-08 11:00:00 | 3020.15000  | 3040.30000  | 3010.20000  | 3035.45000  | 450.2500000000
3         | 2025-06-08 10:00:00 | 600.75000   | 610.90000   | 595.60000   | 605.30000   | 2000.0000000000
3         | 2025-06-08 11:00:00 | 605.30000   | 615.25000   | 600.10000   | 612.45000   | 1800.5000000000
4         | 2025-06-08 10:00:00 | 1.85000     | 1.92000     | 1.80000     | 1.90000     | 100000.0000000000
4         | 2025-06-08 11:00:00 | 1.90000     | 1.95000     | 1.87000     | 1.93000     | 95000.0000000000
5         | 2025-06-08 10:00:00 | 0.95000     | 0.98000     | 0.93000     | 0.96000     | 500000.0000000000
5         | 2025-06-08 11:00:00 | 0.96000     | 0.99000     | 0.95000     | 0.97000     | 480000.0000000000
```

### 4.5 持倉表（holdings）

| 欄位名稱       | 類型      | 描述         |
|----------------|-----------|--------------|
| id             | INT       | 持倉 ID（主鍵） |
| user_id        | INT       | 使用者 ID（外鍵） |
| crypto_id      | INT       | 幣種 ID（外鍵） |
| amount         | DECIMAL   | 持有數量       |
| avg_buy_price  | DECIMAL   | 持倉均價       |

#### 完整性限制說明

**id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），自動遞增（AUTO_INCREMENT）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 0 到 2,147,483,647，從 1 開始
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**user_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES users(id) ON DELETE CASCADE）
- 是否可重複：允許重複
- 長度限制：INT，與 users.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**crypto_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES cryptos(id) ON DELETE CASCADE）
- 是否可重複：允許重複
- 長度限制：INT，與 cryptos.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**amount**：
- 約束：非空（NOT NULL），CHECK (amount >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(20, 10)，總長 20 位，含 10 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(20, 10)，固定精度十進位數

**avg_buy_price**：
- 約束：非空（NOT NULL），CHECK (avg_buy_price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

#### 舉例

```
id | user_id | crypto_id | amount           | avg_buy_price
---+---------+-----------+-----------------+---------------
1  | 1       | 1         | 0.5000000000    | 58000.00000
2  | 2       | 2         | 10.0000000000   | 2900.00000
3  | 3       | 3         | 15.0000000000   | 590.00000
4  | 4       | 4         | 1000.0000000000 | 1.70000
5  | 5       | 5         | 5000.0000000000 | 0.90000
6  | 6       | 6         | 20.0000000000   | 140.00000
7  | 7       | 7         | 50.0000000000   | 19.50000
8  | 8       | 8         | 10000.0000000000| 0.30000
9  | 9       | 9         | 800.0000000000  | 1.10000
10 | 10      | 10        | 40.0000000000   | 24.00000
```

### 4.6 交易紀錄表（transactions）

| 欄位名稱         | 類型        | 描述         |
|------------------|-------------|--------------|
| id               | INT         | 交易 ID（主鍵） |
| user_id          | INT         | 使用者 ID（外鍵） |
| crypto_id        | INT         | 幣種 ID（外鍵） |
| transaction_type | VARCHAR     | 交易類型（買/賣） |
| amount           | DECIMAL     | 交易數量       |
| price            | DECIMAL     | 交易價格       |
| timestamp        | TIMESTAMP   | 交易時間       |

#### 完整性限制說明

**id**：
- 約束：主鍵（PRIMARY KEY），非空（NOT NULL），自動遞增（AUTO_INCREMENT）
- 是否可重複：不可重複
- 長度限制：INT，32 位整數，範圍 -2,147,483,648 到 2,147,483,647
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**user_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES users(id) ON DELETE CASCADE）
- 是否可重複：允許重複
- 長度限制：INT，與 users.id 一致
- 特殊符號限制：僅限整數數值
- 資料型態：INT，整數型態，儲存整數值

**crypto_id**：
- 約束：非空（NOT NULL），外鍵（FOREIGN KEY REFERENCES cryptos(id) ON DELETE CASCADE）
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
- 長度限制：DECIMAL(20, 10)，總長 20 位，含 10 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(20, 10)，固定精度十進位數

**price**：
- 約束：非空（NOT NULL），CHECK (price >= 0)
- 是否可重複：允許重複
- 長度限制：DECIMAL(18, 5)，總長 18 位，含 5 位小數
- 特殊符號限制：僅限數字、小數點
- 資料型態：DECIMAL(18, 5)，固定精度十進位數

**timestamp**：
- 約束：非空（NOT NULL），DEFAULT CURRENT_TIMESTAMP
- 是否可重複：允許重複
- 長度限制：TIMESTAMP，範圍 1970-01-01 00:00:01 到 2038-01-19 03:14:07 UTC
- 特殊符號限制：格式 YYYY-MM-DD HH:MM:SS，僅限數字、連字符、冒號、空格
- 資料型態：TIMESTAMP，時間戳型態，儲存日期和時間

#### 舉例

```
id | user_id | crypto_id | transaction_type | amount           | price       | timestamp
---+---------+-----------+------------------+-----------------+-------------+-------------------------
1  | 1       | 1         | buy              | 0.5000000000    | 58000.00000 | 2025-05-01 10:00:00
2  | 2       | 2         | buy              | 10.0000000000   | 2900.00000  | 2025-05-02 12:00:00
3  | 3       | 3         | buy              | 15.0000000000   | 590.00000   | 2025-05-03 14:30:00
4  | 4       | 4         | buy              | 1000.0000000000 | 1.70000     | 2025-05-04 09:15:00
5  | 5       | 5         | buy              | 5000.0000000000 | 0.90000     | 2025-05-05 11:45:00
6  | 6       | 6         | buy              | 20.0000000000   | 140.00000   | 2025-05-06 16:20:00
7  | 7       | 7         | sell             | 25.0000000000   | 21.00000    | 2025-05-07 08:00:00
8  | 8       | 8         | buy              | 10000.0000000000| 0.30000     | 2025-05-08 13:10:00
9  | 9       | 9         | sell             | 400.0000000000  | 1.25000     | 2025-05-09 15:25:00
10 | 10      | 10        | buy              | 40.0000000000   | 24.00000    | 2025-05-10 17:50:00
```
## 5. 資料庫 Schema (SQL)

### 創建資料表

```sql
-- 使用者表
CREATE TABLE users (
    id INT NOT NULL AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    role VARCHAR(20) NOT NULL CHECK (role IN ('super_admin', 'admin', 'user')),
    PRIMARY KEY (id),
    UNIQUE (email)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 使用者憑證表
CREATE TABLE user_credentials (
    user_id INT NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    PRIMARY KEY (user_id),
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 幣種表
CREATE TABLE cryptos (
    id INT NOT NULL AUTO_INCREMENT,
    symbol VARCHAR(10) NOT NULL UNIQUE,
    name VARCHAR(50) NOT NULL,
    current_price DECIMAL(18, 5) NOT NULL CHECK (current_price >= 0),
    PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 歷史價格表
CREATE TABLE crypto_prices (
    crypto_id INT NOT NULL,
    timestamp TIMESTAMP NOT NULL,
    open_price DECIMAL(18, 5) NOT NULL CHECK (open_price >= 0),
    high_price DECIMAL(18, 5) NOT NULL CHECK (high_price >= 0),
    low_price DECIMAL(18, 5) NOT NULL CHECK (low_price >= 0),
    close_price DECIMAL(18, 5) NOT NULL CHECK (close_price >= 0),
    volume DECIMAL(20, 10) NOT NULL CHECK (volume >= 0),
    PRIMARY KEY (crypto_id, timestamp),
    FOREIGN KEY (crypto_id) REFERENCES cryptos(id) ON DELETE CASCADE,
    INDEX idx_timestamp (timestamp)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 持倉表
CREATE TABLE holdings (
    id INT NOT NULL AUTO_INCREMENT,
    user_id INT NOT NULL,
    crypto_id INT NOT NULL,
    amount DECIMAL(20, 10) NOT NULL CHECK (amount >= 0),
    avg_buy_price DECIMAL(18, 5) NOT NULL CHECK (avg_buy_price >= 0),
    PRIMARY KEY (id),
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (crypto_id) REFERENCES cryptos(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- 交易紀錄表
CREATE TABLE transactions (
    id INT NOT NULL AUTO_INCREMENT,
    user_id INT NOT NULL,
    crypto_id INT NOT NULL,
    transaction_type VARCHAR(10) NOT NULL CHECK (transaction_type IN ('buy', 'sell')),
    amount DECIMAL(20, 10) NOT NULL CHECK (amount > 0),
    price DECIMAL(18, 5) NOT NULL CHECK (price >= 0),
    timestamp TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id),
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (crypto_id) REFERENCES cryptos(id) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```
## 6. 視圖 (View)

### 6.1 使用者管理
**需求**：
- 註冊與登錄：電子郵件與密碼註冊、登錄，支援密碼重置。
- 個人資料管理：查看與更新 username、email。
- 區分一般使用者、管理員與超級管理員。

#### 使用者資料視圖（v_user_profile）
- **用途**：
  - 為一般使用者提供個人資料檢視，支援查看與更新 `username` 和 `email`。
  - 管理員與超級管理員可查詢所有用戶資料，支援用戶管理。
- **基於表**：`users`
- **欄位**：
  - user_id (INT)：用戶 ID
  - username (VARCHAR)：使用者名稱
  - email (VARCHAR)：電子郵件
  - role (VARCHAR)：角色（user、admin、super_admin）
- **SQL**：
  ```sql
  CREATE VIEW v_user_profile AS
  SELECT 
      id AS user_id,
      username,
      email,
      role
  FROM users;
  ```
- **應用場景**：
  - **一般使用者**：查看自身資料：
    ```sql
    SELECT * FROM v_user_profile WHERE user_id = ?;
    ```
  - **管理員**：檢視用戶清單：
    ```sql
    SELECT * FROM v_user_profile WHERE role = 'user';
    ```
  - **超級管理員**：分配角色：
    ```sql
    SELECT * FROM v_admin_users ORDER BY user_id;
    ```
- **說明**：
  - 簡化個人資料查詢，隱藏底層結構，符合個人資料管理需求。
  - 支援權限分級限制存取。
  - 提供管理者管理介面。


### 6.2 資產管理
**需求**：
- 查看當前持有的所有幣種及其數量。
- 計算每種投資幣種的盈虧。
- 新增或移除持有的幣種。
- 查看投資分析報告。

#### (1) 持倉概覽視圖（v_user_holdings）
- **用途**：
  - 為一般使用者提供持倉詳情，顯示數量、市值、均價與盈虧。
  - 支援實時追蹤，計算最新市值與盈虧。
  - 管理員與超級管理員可監控用戶持倉。
- **基於表**：`holdings`、`cryptos`
- **欄位**：
  - user_id (INT)：用戶 ID
  - crypto_id (INT)：幣種 ID
  - symbol (VARCHAR)：幣種代號
  - amount (DECIMAL(20,10))：持倉數量
  - avg_buy_price (DECIMAL(18,5))：平均買入價格
  - current_price (DECIMAL(18,5))：當前價格
  - market_value (DECIMAL(20,10))：市值
  - profit_loss (DECIMAL(20,10))：盈虧
- **SQL**：
  ```sql
  CREATE VIEW v_user_holdings AS
  SELECT 
      h.user_id,
      h.crypto_id,
      c.symbol,
      h.amount,
      h.avg_buy_price,
      c.current_price,
      ROUND(h.amount * c.current_price, 10) AS market_value,
      ROUND(h.amount * (c.current_price - h.avg_buy_price), 10) AS profit_loss
  FROM holdings h
  JOIN cryptos c ON h.crypto_id = c.id;
  ```
- **應用場景**：
  - **一般使用者**：查看持倉：
    ```sql
    SELECT * FROM v_user_holdings WHERE user_id = ? ORDER BY market_value DESC;
    ```
  - **管理員**：監控大額持倉：
    ```sql
    SELECT * FROM v_user_holdings WHERE market_value > 1000000;
    ```
  - **報告生成**：計算總市值：
    ```sql
    SELECT SUM(market_value) AS total_value, SUM(profit_loss) AS total_profit
    FROM v_user_holdings WHERE user_id = ?;
    ```
- **說明**：
  - 整合持倉與行情數據，計算市值與盈虧，滿足持倉追蹤需求。
  - 支援新增/移除幣種的後續操作，簡化報告生成。

#### (2) 投資表現視圖（v_user_investment_performance）
- **用途**：
  - 提供投資表現分析，顯示收益與投資回報率（ROI）。
  - 結合歷史價格計算特定時間段的收益。
  - 支援管理員分析用戶投資表現。
- **基於表**：`holdings`、`cryptos`、`crypto_prices`
- **欄位**：
  - user_id (INT)：用戶 ID
  - crypto_id (INT)：幣種 ID
  - symbol (VARCHAR)：幣種代號
  - amount (DECIMAL(20,10))：持倉數量
  - avg_buy_price (DECIMAL(18,5))：平均買入價格
  - current_price (DECIMAL(18,5))：當前價格
  - historical_price (DECIMAL(18,5))：歷史價格（30 天前）
  - current_profit (DECIMAL(20,10))：當前盈虧
  - historical_profit (DECIMAL(20,10))：歷史盈虧
  - roi (DECIMAL(10,2))：投資回報率（%）
- **SQL**：
  ```sql
  CREATE VIEW v_user_investment_performance AS
  SELECT 
      h.user_id,
      h.crypto_id,
      c.symbol,
      h.amount,
      h.avg_buy_price,
      c.current_price,
      COALESCE((
          SELECT close_price 
          FROM crypto_prices 
          WHERE crypto_id = h.crypto_id 
          AND timestamp = DATE_SUB(CURDATE(), INTERVAL 30 DAY)
          LIMIT 1
      ), c.current_price) AS historical_price,
      ROUND(h.amount * (c.current_price - h.avg_buy_price), 10) AS current_profit,
      ROUND(h.amount * (COALESCE((
          SELECT close_price 
          FROM crypto_prices 
          WHERE crypto_id = h.crypto_id 
          AND timestamp = DATE_SUB(CURDATE(), INTERVAL 30 DAY)
          LIMIT 1
      ), c.current_price) - h.avg_buy_price), 10) AS historical_profit,
      ROUND(
          (h.amount * (c.current_price - h.avg_buy_price)) / 
          (h.amount * h.avg_buy_price) * 100, 
          2
      ) AS roi
  FROM holdings h
  JOIN cryptos c ON h.crypto_id = c.id;
  ```
- **應用場景**：
  - **一般使用者**：查看投資表現：
    ```sql
    SELECT * FROM v_user_investment_performance WHERE user_id = ?;
    ```
  - **管理員**：分析投資：
    ```sql
    SELECT SUM(current_profit) AS total_profit, AVG(roi) AS avg_roi
    FROM v_user_investment_performance GROUP BY user_id;
    ```
- **說明**：
  - 計算當前與歷史收益，支援 ROI 分析，滿足投資表現需求。
  - 提供自訂時間範圍的基礎，簡化報告生成邏輯。

### 6.3 交易紀錄
**需求**：
- 記錄買入與賣出交易（幣種、數量、價格、時間）。
- 提供交易歷史查詢功能。

#### 交易歷史視圖（v_user_transactions）
- **用途**：
  - 為一般使用者提供交易歷史查詢，顯示買入/賣出詳情。
  - 管理員與超級管理員可監控所有交易。
- **基於表**：`transactions`、`cryptos`、`users`
- **欄位**：
  - transaction_id (INT)：交易 ID
  - user_id (INT)：用戶 ID
  - username (VARCHAR)：使用者名稱
  - crypto_id (INT)：幣種 ID
  - symbol (VARCHAR)：幣種代號
  - transaction_type (VARCHAR)：交易類型
  - amount (DECIMAL(20,10))：交易數量
  - price (DECIMAL(18,5))：交易價格
  - total_cost (DECIMAL(20,10))：總成本
  - timestamp (TIMESTAMP)：交易時間
- **SQL**：
  ```sql
  CREATE VIEW v_user_transactions AS
  SELECT 
      t.id AS transaction_id,
      t.user_id,
      u.username,
      t.crypto_id,
      c.symbol,
      t.transaction_type,
      t.amount,
      t.price,
      ROUND(t.amount * t.price, 10) AS total_cost,
      t.timestamp
  FROM transactions t
  JOIN users u ON t.user_id = u.id
  JOIN cryptos c ON t.crypto_id = c.id;
  ```
- **應用場景**：
  - **一般使用者**：查看交易：
    ```sql
    SELECT * FROM v_user_transactions 
    WHERE user_id = ? AND timestamp BETWEEN ? AND ? 
    ORDER BY timestamp DESC;
    ```
  - **管理員**：監控交易：
    ```sql
    SELECT * FROM v_user_transactions 
    WHERE total_cost > 100000 
    ORDER BY timestamp DESC;
    ```
- **說明**：
  - 整合交易與用戶、幣種資訊，計算總成本，滿足交易查詢需求。
  - 支援管理員監控大額交易，符合權限設定。

### 6.4 市場資訊與分析
**需求**：
- 實時行情：查看幣種價格、24小時漲跌幅。
- 歷史價格：查看 K 線圖（1小時、4小時、日線），計算技術指標。

#### (1) 實時行情視圖（v_market_realtime）
- **用途**：
  - 提供即時行情，顯示價格與 24 小時漲跌幅。
  - 支援管理員監控市場動態。
- **基於表**：`cryptos`、`crypto_prices`
- **欄位**：
  - crypto_id (INT)：幣種 ID
  - symbol (VARCHAR)：幣種代號
  - name (VARCHAR)：幣種名稱
  - current_price (DECIMAL(18,5))：當前價格
  - price_24h_ago (DECIMAL(18,5))：24 小時前價格
  - price_change_24h (DECIMAL(10,2))：漲跌幅（%）
- **SQL**：
  ```sql
  CREATE VIEW v_market_realtime AS
  SELECT 
      c.id AS crypto_id,
      c.symbol,
      c.name,
      c.current_price,
      COALESCE((
          SELECT close_price 
          FROM crypto_prices 
          WHERE crypto_id = c.id 
          AND timestamp = DATE_SUB(NOW(), INTERVAL 24 HOUR)
          LIMIT 1
      ), c.current_price) AS price_24h_ago,
      ROUND(
          ((c.current_price - COALESCE((
              SELECT close_price 
              FROM crypto_prices 
              WHERE crypto_id = c.id 
              AND timestamp = DATE_SUB(NOW(), INTERVAL 24 HOUR)
              LIMIT 1
          ), c.current_price)) / 
          COALESCE((
              SELECT close_price 
              FROM crypto_prices 
              WHERE crypto_id = c.id 
              AND timestamp = DATE_SUB(NOW(), INTERVAL 24 HOUR)
              LIMIT 1
          ), c.current_price)) * 100, 
          2
      ) AS price_change_24h
  FROM cryptos c;
  ```
- **應用場景**：
  - **一般使用者**：查看行情：
    ```sql
    SELECT * FROM v_market_realtime ORDER BY price_change_24h DESC;
    ```
  - **管理員**：監控市場：
    ```sql
    SELECT * FROM v_market_realtime WHERE ABS(price_change_24h) > 10;
    ```
- **說明**：
  - 計算 24 小時漲跌幅，滿足實時行情需求。
  - 支援排序與篩選，方便識別市場動態。

#### (2) K 線圖視圖（v_kline_data）
- **用途**：
  - 提供歷史價格數據，支援 K 線圖與技術指標計算。
  - 管理員可分析市場趨勢。
- **基於表**：`crypto_prices`、`cryptos`
- **欄位**：
  - crypto_id (INT)：幣種 ID
  - symbol (VARCHAR)：幣種代號
  - timestamp (TIMESTAMP)：時間點
  - open_price (DECIMAL(18,5))：開盤價
  - high_price (DECIMAL(18,5))：最高價
  - low_price (DECIMAL(18,5))：最低價
  - close_price (DECIMAL(18,5))：收盤價
  - volume (DECIMAL(20,10))：交易量
- **SQL**：
  ```sql
  CREATE VIEW v_kline_data AS
  SELECT 
      cp.crypto_id,
      c.symbol,
      cp.timestamp,
      cp.open_price,
      cp.high_price,
      cp.low_price,
      cp.close_price,
      cp.volume
  FROM crypto_prices cp
  JOIN cryptos c ON cp.crypto_id = c.id;
  ```
- **應用場景**：
  - **一般使用者**：生成 K 線圖：
    ```sql
    SELECT * FROM v_kline_data 
    WHERE crypto_id = 1 AND timestamp >= '2025-06-01' 
    ORDER BY timestamp;
    ```
  - **技術指標**：計算 RSI：
    ```sql
    SELECT close_price 
    FROM v_kline_data 
    WHERE crypto_id = 1 
    ORDER BY timestamp DESC LIMIT 14;
    ```
  - **管理員**：分析市場：
    ```sql
    SELECT symbol, AVG(volume) AS avg_volume 
    FROM v_kline_data 
    WHERE timestamp >= DATE_SUB(NOW(), INTERVAL 7 DAY)
    GROUP BY crypto_id, symbol;
    ```
- **說明**：
  - 支援 K 線圖與技術指標，滿足歷史價格需求。
  - 結合 `cryptos.symbol` 提升顯示友好性。

### 6.5 視圖總覽與權限

| 視圖名稱                     | 功能需求         | 適用角色                     | 基於表                        |
|------------------------------|------------------|------------------------------|-------------------------------|
| v_user_profile              | 使用者管理       | User, Admin, Super Admin     | users                         |                       
| v_user_holdings             | 資產管理         | User, Admin, Super Admin     | holdings, cryptos             |
| v_user_investment_performance | 資產管理       | User, Admin, Super Admin     | holdings, cryptos, crypto_prices |
| v_user_transactions         | 交易紀錄         | User, Admin, Super Admin     | transactions, users, cryptos  |
| v_market_realtime           | 市場資訊與分析   | User, Admin, Super Admin     | cryptos, crypto_prices        |
| v_kline_data                | 市場資訊與分析   | User, Admin, Super Admin     | crypto_prices, cryptos        |


## 7. 團隊分工

* **組長**：王忠仁（boxcat-none）
  **工作內容**：自我介紹、功能特色、系統需求、資料庫結構、完整性限制說明、舉例、資料庫Schema(SQL)、視圖(View)

* **組員**：張家誠（Adsgfjhk）
  **工作內容**：自我介紹、ER Diagram、功能特色、系統需求

* **組員**：劉向宏（liuleo0518）
  **工作內容**：自我介紹、資料庫結構、舉例、完整性限制說明
---

## 8. 報告連結

## 9. 參考資料
* 使用Grok完成部分說明
