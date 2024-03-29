## 前提
- いつも頭が冴えてるとは限らない。調子が悪い日も考慮する。
- 画面や機能ごとに行い、時間単位ではなく日単位で見積もる。見積もる際は(1,3,5など奇数のみで工数を見積もる。)時間を求められている場合は日で計算してから出す。

## 必要作業

- 環境構築
  - 開発環境
    - 開発用データの管理方法確立
    - CI環境構築
    - Linter設定
    - テストコード実行環境作成
    - Webpackの設定
      - トランスパイル時、ターゲットブラウザ用にベンダープレフィックスの自動付与やpolyfillなどの対応も行う。
  - stg環境
  - 本番環境
- バリデーション(client/server)
  - エラーメッセージの表示
- パッケージの使い方の把握
- メーラー等の設定
- 例外ハンドリング
- テストコード作成
  - 書く時間なくてもどういったケースが必要かだけの定義はしておく。
- コード設計(名前空間やDI方法、クラス設計など)
- プロジェクト固有設定(timezone, locale, .env, environments)
- DB設計(論理、物理共に)
- サーバー構築
- デプロイ方法確立
  - stg, 本番へのデプロイの自動化
- 結合テストシナリオ作成&実施

## プロジェクト環境構築
- 例外ハンドラー

## 各実装で必要な処理
### 環境構築
- メール送信(redis, smtp設定, redisキューイングワーカー)

### ログイン
- セッション有効期限の設定
- エラーメッセージの設定
- ログイン確認処理の共通化
- CSRF対策

### 例外のハンドリング
- 例外の定義
- 例外発生時のrouteと表示画面(404,500,401など)

### メール送信処理
- キューイング(redis等使う)
- メールフォーマット

### API開発
- APIのレスポンスの定義
- エラー時の表記
- API仕様書(swaggerよかった)

### 削除処理
- 論理削除か物理削除か
- 論理削除の場合、論理削除後のデータの取り扱い

### DB設計
- マルチテナントなどの場合シャーディングやパーティションで対応するか管理スキーマで対応するか
- データが何万件と増えた場合どう対応するか
