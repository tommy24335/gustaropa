# README

## アプリケーション名
gustapora

## アプリケーション概要
ファッションECサイト

ユーザー登録
商品出品
画像、動画投稿
商品詳細の確認
商品購入

## URL

##　テスト用アカウント

## 利用方法
1. 新規登録をクリックし、遷移先のページからユーザー情報をを入力して登録してください。
2. 商品出品ボタンをクリックし遷移先のページから、必要な情報を入力して出品してください。
3. 出品された商品の画像をクリックし、商品詳細ページにて「購入する」ボタンを押してください。
4. 購入ページで必要な情報を入力し「購入確定」ボタンを押してください。

## 目指した課題解決
商品を購入するにあたって画像だけでは伝わらない、
サイズ感、素材感であったりを試着動画を一緒に投稿することで、
商品購入に繋げることです。

## 洗い出した要件
ユーザー管理機能
商品出品機能
商品一覧機能
商品詳細表示機能
商品詳細編集機能
商品削除機能
商品購入機能
オープンAPIを利用したクレジットカード決済
コメント機能

## 実装した機能の説明

## 実装予定の機能
商品詳細編集機能
商品削除機能
コメント機能

# データベース設計

## users テーブル

| Column             | Type   | Options                   |
| ------------------ | ------ | ------------------------- |
| nickname           | string | null: false               |
| email              | string | null: false, unique: true |
| encrypted_password | string | null: false               |
| family_name        | string | null: false               |
| last_name          | string | null: false               |
| family_name_kana   | string | null: false               |
| last_name_kana     | string | null: false               |


### アソシエーション
- has_many :items
- has_many :order
- has_many :comments

## addresses テーブル

| Column              | Type       | Options                        |
| ------------------- | ---------- | ------------------------------ |
| address             | string     | null: false                    |
| building_name       | string     |                                |
| city                | string     | null: false                    |
| prefecture_id       | integer    | null: false                    |
| postal_code         | string     | null: false                    |
| phone_number        | string     | null: false                    |
| order               | references | null: false, foreign_key: true |

### アソシエーション
- belongs_to :order

## orders テーブル

| Column           | Type       | Options                            |
| ---------------- | ---------- | -----------------------------------|
| user             | references | null: false, foreign_key: true     |
| item             | references | null: false, foreign_key: true     |

### アソシエーション
- belongs_to :user
- belongs_to :item
- has_one :address

## items テーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| name             | string     | null: false                    |
| price            | integer    | null: false                    |
| description      | text       | null: false                    |
| shipping_cost_id | integer    | null: false                    |
| shipping_day_id  | integer    | null: false                    |
| prefecture_id    | integer    | null: false                    |
| user             | references | null: false, foreign_key: true |
| category_id      | integer    | null: false                    |
| item_status_id   | integer    | null: false                    |

### アソシエーション
- has_one :order
- belongs_to :user
- has_many :comments
- has_many_attached :images
- has_one_attached :video


## comments テーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| text             | text       | null: false                    |
| user             | references | null: false, foreign_key: true |
| item             | references | null: false, foreign_key: true |
|
### アソシエーション
- belongs_to :user
- belongs_to :item