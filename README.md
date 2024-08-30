# shopify_hokusaikan

要参照
https://shopify.dev/docs/themes/getting-started/customize

### Shopify CLI のインストール要件

Shopify CLI をインストールして実行するための要件は、オペレーティング システムによって異なります。

1. windows

- Node.js 18 or higher.
- Ruby+Devkit 3.0, installed using RubyInstaller for Windows
- (select the MSYS2 component and the MSYS2 base installation option)
- Git
- Bundler 2.3.8 or higher

### ステップ 1: 販売者のストアへのアクセスをリクエストする

### ステップ 2: Shopify CLI をインストールする

- npm install -g @shopify/cli @shopify/theme

### ステップ 3: 販売者のテーマ コードをダウンロードする

- shopify theme list --store=b44387-75
- shopify theme pull --store b44387-75 --theme

### ステップ 4：開発する(ヒグチのやり方)

- ブランチ運用
  - feature ブランチで開発し、本番反映前に master ブランチで本番環境の内容を theme download
  - 差分が無いことを確認した上で feature ブランチの内容を theme deploy
  - 一点、 theme watch コマンドの実行中にブランチを切り替えると予期しないファイルまで一気に反映されてしまうので、留意が必要です。
- テーマ開発でもっともバージョン管理が困難なのは、setting_data.json ファイル
  - setting_data.json については git 管理からも Theme Kit 管理からも除外しています。
  - クライアントが本番環境テーマエディタから編集を行う前提で、上書きリスクを鑑み、テスト環境との差分を許容する運用です。
  - なので gitignore に入れてあります

### ステップ 5: 変更をプレビューする

- テーマを変更した後、 を実行して shopify theme dev ブラウザーでテーマを操作できます。Shopify CLI は、接続しているストアにテーマを開発テーマとしてアップロードします。(これ本番環境に反映される)
- shopify theme serve だとローカルでテストできる
- shopify theme list --store=b44387-75：ID リストを取得
- shopify theme pull --store b44387-75 --theme [ID]：本番環境の現在までの変更を取得
- shopify theme push --theme=ID ：反映
- - 反映前にブランチを作成して、その日時点での本番環境のデータをそのブランチに保存しておき、特にマージ等はしないで残しておく
- main に変更が必要な内容があれば main でも取得し、反映したうえでデプロイする

### ステップ 5: 変更をプレビューする
