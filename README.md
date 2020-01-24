# s3-uploader
`AWS S3`にブラウザから画像をアップロードできるようにする業務改善アプリケーション

--- 

## 動かし方

### Amazon Cognito で Identity Pool の作成

[こちら](https://console.aws.amazon.com/cognito/create/?region=us-east-1) から、`Identity Pool` を作成します。
- `name` は任意のものを
- `unauthenticated identities` にチェック（非認証ユーザーの許可）
- 新規ロールを作成し、そのまま許可
- `Cognito Identity Pool ID`をメモしておく

### IAM ロールの設定
- `Amazon S3` にパケットを作成する
- `ヘッダーの名前タブ` > `認証情報` > `ロール` へ移り、`**UnauthRole`を選択
- `ロールポリシーの作成`を選択し、`PolicyGenerator`を選択。順番に
    - `許可`
    - `Amazon S3`
    - `s3:PutObject`, `s3:PutObjectAcl`
    - `arn:aws:s3:::<S3のバケット名>/*`

### S3 のバケット設定
`Amazon S3`のバケットのプロパティにて、`アクセス許可` > `CORS設定の編集` に [CORS Setting](./cors-setting.xml) を入力

### HTML / JavaScriptの設定
1. `index.html` に記載の `Identity Pool Id` と `Bucket Name` を埋める
2. ブラウザにアップロードする
3. 完了！！