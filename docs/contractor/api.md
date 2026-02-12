# Aモジュール - API設計書

## 概要

Aモジュールが提供するREST APIの仕様を定義する。

---

## API一覧

| # | メソッド | エンドポイント | 概要 |
|---|---------|---------------|------|
| 1 | GET | `/api/contractor/{id}` | 契約者情報取得 |
| 2 | PUT | `/api/contractor/{id}` | 契約者情報更新 |
| 3 | POST | `/api/contractor` | 契約者情報登録 |
| 4 | DELETE | `/api/contractor/{id}` | 契約者情報削除 |

---

## 1. 契約者情報取得 API

### リクエスト

- **メソッド**: `GET`
- **パス**: `/api/contractor/{id}`
- **認証**: Bearer Token 必須

### パスパラメータ

| パラメータ | 型 | 必須 | 説明 |
|-----------|-----|------|------|
| id | string | ○ | 契約者ID |

### レスポンス (200 OK)

```json
{
  "contractorId": "C-00001",
  "name": "山田 太郎",
  "email": "yamada@example.com",
  "phone": "090-1234-5678",
  "address": "東京都渋谷区...",
  "contractDate": "2025-04-01",
  "status": "ACTIVE"
}
```

### エラーレスポンス

| ステータス | 説明 |
|-----------|------|
| 400 | リクエスト不正 |
| 401 | 認証エラー |
| 404 | 契約者が存在しない |
| 500 | サーバーエラー |

---

## 2. 契約者情報更新 API

### リクエスト

- **メソッド**: `PUT`
- **パス**: `/api/contractor/{id}`
- **Content-Type**: `application/json`
- **認証**: Bearer Token 必須

### リクエストボディ

```json
{
  "name": "山田 太郎",
  "email": "yamada@example.com",
  "phone": "090-1234-5678",
  "address": "東京都渋谷区..."
}
```

| フィールド | 型 | 必須 | 最大長 | 説明 |
|-----------|-----|------|--------|------|
| name | string | ○ | 100 | 契約者名 |
| email | string | ○ | 256 | メールアドレス |
| phone | string | - | 20 | 電話番号 |
| address | string | - | 500 | 住所 |

### レスポンス (200 OK)

```json
{
  "contractorId": "C-00001",
  "message": "更新が完了しました"
}
```

---

## 3. 契約者情報登録 API

### リクエスト

- **メソッド**: `POST`
- **パス**: `/api/contractor`
- **Content-Type**: `application/json`

### リクエストボディ

```json
{
  "name": "鈴木 花子",
  "email": "suzuki@example.com",
  "phone": "080-9876-5432",
  "address": "大阪府大阪市..."
}
```

### レスポンス (201 Created)

```json
{
  "contractorId": "C-00002",
  "message": "登録が完了しました"
}
```

---

## 共通ヘッダー

| ヘッダー | 値 | 説明 |
|---------|-----|------|
| Authorization | `Bearer {token}` | 認証トークン |
| Content-Type | `application/json` | リクエスト形式 |
| X-Request-Id | UUID | リクエスト追跡用ID |
