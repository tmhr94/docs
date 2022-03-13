クラスをDIすることによりクラスのパブリックインターフェースのみに依存することができる。そのクラスがクラスを知っておく必要がなくなる

テストはパブリックインターフェースのみテストすべき

ポリモーフィズム
https://qiita.com/Nossa/items/a93024e653ff939115c6

委譲
https://qiita.com/w650/items/671cc9c49b2ebf60620d

# rails

accepts_nested_attributes_forで関連レコードも作成時、validationはcontextで関連レコードも切替可能。
person.save!(context: :account_setup)

accepts_nested_attributes_forは更新時、テーブルにidがある前提なのでidカラムがない場合は、idカラムを追加するか、 `self.primary_key` で明示的にプライマリキーを指定しなければいけない。

サービス、モデル、FormObjectは以下それぞれの認識だったのですが、こちらご意見伺いたいです:bow:

- サービス: 複雑なビジネスロジック担当(モデルのCRUDのメソッドなどを駆使してビジネスロジックを実現する)。コントローラーが複雑になった場合に使用する。
- モデル: モデルに関する処理。CRUDなど。
- FormObject: モデルにフォームやバッチなどのケースごとの固有の処理(以下参照)が定義される場合、他のケースの処理でこの固有の処理をハンドリングしなければいけない状態になることを回避する目的で使用する。
https://lifood.esa.io/posts/159#%E9%96%A2%E9%80%A3%E3%83%A1%E3%83%A2

form objectでバリデーションコンテキスト削除
https://techracho.bpsinc.jp/hachi8833/2018_05_15/56271

そのためビジネスロジックをコーディングする目的のためだけにFormObjectは使用しない想定でした。FormObject内でも複雑なビジネスロジックを実現する場合はサービスをコールする想定でした。


    - **FormObjectは以下の場面で使用する想定にFixed**
        1. フォーム固有のバリデーションがある場合( `validation context` の辛み解消)
            - 例: 新規作成の場合だけとあるバリデーションが必要
        2. フォーム固有のコールバックを含む処理をモデルに書かないといけなくなった時
            - 他のロジックで同一モデルを扱う場合にハンドリングが必要となるためFormObjectに分離
         3. モデルの各カラムの値とビューのフォームと値が同一とならない時( `nested_attirbutes_for` などで素直に値を入れられない時)
             - FormObjectがビューのフォームと1:1となることでフォーム用に値を変換する処理などをモデルやコントローラーに書かなくて済む。
         - 備考1: フォームに限らず、バッチ処理などでも上記3つに当てはまる場合、FormObjectライクなクラスで処理を定義する。同様の辛み解消目的。
         
         

form objectで accept_nested_attirbutes_for
https://medium.com/@jaryl/disciplined-rails-form-object-techniques-patterns-part-2-12b8d530143d

rubyでメソッドジャンプwith VSCode
https://sunday-morning.app/posts/2020-08-15-vscode-ruby-solargraph


rails 遅いクエリ発見
https://google.github.io/sqlcommenter/

メールテスト
https://github.com/mailhog/MailHog

cancancanはこれを見れば大丈夫。http://greena13.github.io/blog/2019/07/12/cancancan-cheatsheet/

### accepts_nested_attributes_for
バリデーションエラーにインデックス設定
https://qiita.com/kano-e/items/ecd7773ab817fd1e6e07

validates_associated
https://qiita.com/a2cfry/items/99c811938e2cf20a35f5

delegateでデメテルの法則に遵守する場合、view側は除外する。view側はメソッドチェーンでアクセスして良い。


# rspec
https://qiita.com/muran001/items/276b3375e3e37de368e6

# テーブル設計
https://spice-factory.co.jp/development/has-and-belongs-to-many-table/

---

validationはcontextを使って用途ごとに分ける。
コントローラーはserviceを使う。
validationは分けても良いけどモデルのままでも良いかも？
ビジネスロジックはserviceで定義。

interactorでビジネスロジックを実装。
interactor内でvalidationは他クラスに任せる。(もしくはモデルに定義し、コンテキストで用途ごとに管理)

これでcrud時のviewに渡るモデルオブジェクトはARのオブジェクトになるのでdraperが使える。
validationはinteractorコール時、validatorをDIしてinteractor内でvalid?をvalidatorに処理委譲。ビジネスロジックで使用するモデルの処理(scopeやデータのCRUDなど)はモデルに直接定義。もしくはモデル内でPOROに処理を委譲しても良い。

ビジネスロジックについて:
https://qiita.com/os1ma/items/25725edfe3c2af93d735

やはりvalidationは外だしするのではなく、責務ごとに切り分けた方が良い。外だしはrubocopの警告回避以外にあまりメリットがないかもしれない？
formオブジェクトを使う。
draper問題は `to_model` メソッドでモデルオブジェクトに変換出来るので問題なし。
formオブジェクトはバリデーションのみを責務とし処理はinteractorに任せる。interactorの処理内で起こる例外以外のエラーはformオブジェクトのエラーに格納する。

参考:
https://naokirin.hatenablog.com/entry/2019/05/03/214107

to_modelについて
https://techracho.bpsinc.jp/hachi8833/2018_03_02/51350

rails デザインパターン
https://product-development.io/posts/rails-design-patterns#validator%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88

1.formオブジェクトの目的
バリデーションをformのユースケースごとに切り分けることが出来る。
これによりmodelに定義してcontextで切り分けて乱雑になることを防ぐことが出来る。コールバックも同様。

2.draperの目的
プレゼンテーション層に関するロジックをモデルから切り離すことで責務を分散出来る。
また、定義を一箇所にまとめておくことで修正漏れを防ぐことが出来る。

3.interactorの目的
ビジネスロジックに関する処理を開発者で共通のインターフェースにて統一することが出来る。命名規則、粒度、目的の統一化、

**単体テストがしやすいか？という着眼点が一番重要。**
単体テストしやすいものはDIを使用していて他クラスと蘇結合で(ダブルで代用オブジェクトが作成出来る)凝集度が高い。

https://moneyforward.com/engineers_blog/2018/12/15/formobject/

fat モデル参考
https://blog.toshimaru.net/how-to-deal-with-fat-model/#interactor

https://medium.com/@jiraffestaff/fat-model-%E3%82%92%E3%82%B5%E3%83%96%E3%82%AF%E3%83%A9%E3%82%B9%E3%81%AB%E5%88%86%E5%89%B2%E3%81%99%E3%82%8B-4fc5aef3d84

https://tech.kitchhike.com/entry/2018/02/28/221159

sentry とは？
mackerelとは？

railsの省メモリ
https://blog.toshimaru.net/rails-batch-optimization/
