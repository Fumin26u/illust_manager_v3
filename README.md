# illust_manager v3
## README
- 名前の通り画像管理システム
- ローカルで動作します。事故が怖いのでWeb上に公開とかはしない予定
- 制作時期: 2024年～ (gptがメタになってから)

## 概要
- いろいろ画像管理システム
  - 各種SNSから画像を自動DLする
  - ローカルの画像からタグを生成する
  - 画像とタグを紐づけてDBに格納する
  - etc

## Image Manager
ローカルにある画像に対して、[Deepdanbooru](https://github.com/KichangKim/DeepDanbooru)を用いて、
イラストにタグ付与を行い、DBに紐づける形で登録します。
以下はWIP
- タグを基準にした画像ソート
- 手動で画像にタグを付与してDeepdanbooruに学習させる
  - ローカルのDeepdanbooruに対して学習させるのみでpublicにはしない 

## ImageDLer
- Twitter(現X)・pixivの画像をまとめて取得・ダウンロードするツールです。
- 指定したユーザーIDの、Twitterは「いいね」、pixivは「ブックマーク」・「ポスト」の画像一覧を取得できます。
- pixivの投稿取得には[pixivpy](https://github.com/upbit/pixivpy)モジュールを利用しています。

## セットアップ

### 1. 設定ファイルの準備

`api/config/` 配下のテンプレートファイルをコピーして実際の値を入力してください。

```bash
cp api/config/mysql.template.py api/config/mysql.py
cp api/config/origin.template.py api/config/origin.py
cp api/config/deepdanbooru.template.py api/config/deepdanbooru.py
```

| ファイル | 設定内容 |
|---|---|
| `api/config/mysql.py` | MySQLの接続情報 (host, user, password, database) |
| `api/config/origin.py` | CORSで許可するオリジン (例: `http://localhost:8080`) |
| `api/config/deepdanbooru.py` | Deepdanbooruモデルのディレクトリパス |

### 2. 環境変数の準備

`.env.example` をコピーして値を入力してください。

```bash
cp .env.example .env
```

| 変数名 | 内容 |
|---|---|
| `SECRET_KEY` | Flaskのシークレットキー |
| `PIXIVPY_REFRESH_TOKEN` | pixivpyのリフレッシュトークン |
| `TEL` | Twitter(X)のアカウント電話番号 |
