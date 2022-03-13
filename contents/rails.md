### Fatモデルについて
ファットモデルは目指すべきものなので、ファットモデル自体が問題ではない。(コントローラーを薄く、モデルを厚くがRailsのデファクト)
モデルに書くべきでない処理を書くということが問題。モデルに書くべき処理によってコード量が多いのであれば、それは問題ではない。

#### Fatモデルの対策方法
1. ViewModelとしてdraperなどを用い、ビューと結合する処理を分ける。
2. とあるユースケースごとのコールバックやバリデーションなどはユースケースごとに定義する。これによりユースケースと密結合となる処理がモデルから消える。Formオブジェクトなど。これによりモデルのテストがしやすくなる。コールバックなどの管理をしなくて済む。

### デザインパターン
導入するデザインパターン

正直、[ここ](https://product-development.io/posts/rails-design-patterns)に書いてあるのどれも良さそう。バリューオブジェクトはちょっと大変そうだけど。

#### Decoratorパターン
ViewModelとしてモデルオブジェクトのViewに関する処理を切り出す。
使用gem: [draper](https://github.com/drapergem/draper)

#### Formオブジェクト
モデルからフォーム(とあるユースケース専用の)バリデーションの責務を切り出す。これによりコールバックの管理やコンテキストでバリデーションを切り分けるなど行わなくて済む。フォームの構造とモデルが密結合した状況を避ける目的。

[formオブジェクトとdraperの共存について](https://web-salad.hateblo.jp/entry/2014/05/22/005754)

#### interactorパターン
複雑なビジネスロジックを実装する。

使用gem: [interactor](https://github.com/collectiveidea/interactor)

### デバッグ
#### gem
gemのデバッグはモンキーパッチを作成し、この中でbyebugを行う。
もしくは、byebugのステップ実行でgemまで進み、行う。(こちらの方が楽ですね。)

### gem
- cancancan
  - 権限管理
- rolify
  - ロール管理
- ransack
  - 検索処理簡易化
- paper_trail
  - 監査ログやバージョン管理機能

#### 開発
- bullet
  - N+1問題可視化
- better_errors
  - エラー表示を見やすく
- rubocop, rubocop-rails, rubocop-performance
  - linter
- brakeman
  - 脆弱性発見
- byebug
  - debug用
- rails_best_practices
  - Railsのベストプラクティスに則っているか確認

#### テスト
- rspec-rails
- factory_bot_rails
- faker
