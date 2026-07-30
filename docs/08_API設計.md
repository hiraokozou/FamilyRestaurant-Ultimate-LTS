# FamilyRestaurant-Ultimate-LTS
# API設計書

---

# 1. 目的

本設計書では、

ブラウザ

↓

Node.js

↓

SQLite

の通信仕様(API)を定義する。

APIはREST形式を採用する。

通信形式はJSONとする。

---

# 2. API一覧

|API|内容|
|---|---|
|GET /api/menu|メニュー取得|
|GET /api/menu/:id|商品詳細|
|POST /api/order|注文|
|GET /api/order/:id|注文確認|
|POST /api/call|店員呼び出し|
|POST /api/payment|会計依頼|
|GET /api/table|テーブル一覧|
|GET /api/kitchen|厨房注文|
|POST /api/kitchen/complete|完成通知|
|GET /api/admin/products|商品管理|
|POST /api/admin/products|商品追加|
|PUT /api/admin/products/:id|商品編集|
|DELETE /api/admin/products/:id|商品削除|
|GET /api/settings|設定取得|
|PUT /api/settings|設定保存|

---

# 3. メニュー取得

GET

```
/api/menu
```

返却例

```json
[
 {
   "id":1,
   "name":"チーズハンバーグ",
   "price":890,
   "image":"hamburg.jpg"
 }
]
```

---

# 4. 商品詳細

GET

```
/api/menu/1
```

返却例

```json
{
 "id":1,
 "name":"チーズハンバーグ",
 "price":890,
 "description":"人気No.1",
 "cook_time":12
}
```

---

# 5. 注文

POST

```
/api/order
```

送信例

```json
{
 "table":1,
 "items":[
   {
     "product":1,
     "quantity":2
   }
 ]
}
```

返却

```json
{
 "result":"OK",
 "order_id":12345
}
```

---

# 6. 店員呼び出し

POST

```
/api/call
```

送信

```json
{
 "table":1,
 "message":"呼び出し"
}
```

---

# 7. 会計依頼

POST

```
/api/payment
```

送信

```json
{
 "table":1
}
```

---

# 8. 厨房

GET

```
/api/kitchen
```

取得

注文一覧

調理時間

状態

---

POST

```
/api/kitchen/complete
```

送信

```json
{
 "order":120
}
```

---

# 9. 商品管理

GET

```
/api/admin/products
```

一覧取得

---

POST

```
/api/admin/products
```

追加

---

PUT

```
/api/admin/products/5
```

編集

---

DELETE

```
/api/admin/products/5
```

削除

---

# 10. 設定

GET

```
/api/settings
```

取得

---

PUT

```
/api/settings
```

保存

---

# 11. エラー

返却例

```json
{
 "success":false,
 "message":"商品が存在しません"
}
```

---

# 12. 成功

返却例

```json
{
 "success":true
}
```

---

# 13. 共通ルール

すべてJSON通信

UTF-8

HTTP Statusを使用

200

400

401

403

404

500

---

# 14. 将来追加API

予約

順番待ち

クーポン

ポイント

分析

AI

Family Pay連携

通知

---

# 15. 開発方針

APIは役割ごとに分離し、

フロントエンド・バックエンドを独立して開発できる構造とする。
