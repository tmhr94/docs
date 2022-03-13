### コミット粒度

一つの機能単位で行う。

```
例:
-> ユーザー登録処理

-> ユーザー登録時のバリデーション処理
```

あるコミットにcheckoutした際、正常に動くようにする。
また、tempとしてコミットしておいたり、上記が担保出来ない場合、rebaseしてコミットを修正する。

### コミットメッセージ

最低限、「何をどうしたか」くらいの情報は入れよう。参考: `[add] packages [XX, YY]`

### 作業ブランチへの他ブランチの統合

他開発者のブランチは、基本 merge ではなく、rebase を使う。

コミットログにマージコミットが混在するのを防ぐ。

### git client
`tig` 使う。

`tig` のショートカットキー

```bash
y -> stash表示
stash表示時:
A -> stash適用
! -> stash削除

---

s -> commit画面表示
enter -> 差分表示
差分表示時:
1 -> ハイライトしている行のみコミット

=

u -> commit/uncommit
! -> 差分削除

---
```

### よく使うコマンド

```
$ git commit
$ git stash save
$ git rebase -i [commit hash]
$ git rebase --continue
$ git commit --amend
$ git push origin -f
$ git rebase -i master
```
