# 前提
VSCodeを使う。

## VSCode
### ショートカット(for Mac)
[参考](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)

- `cmd + d`: 複数選択
- `cmd + p`: ファイルジャンプ
- `cmd + o`: ファイルを開く
- `cmd + shift + f`: 全ファイル内検索
- `ctrl + cmd + e`: 左パネルに移動。再度実行で右パネルに戻る(vimライクに移動可能)
- `ctrl + c`: ファイルの相対パスコピー(左パネルフォーカス時)
- `cmd + j`: Go to Definition
- `cmd + l`: URLを開く
- `cmd + i`: サジェスト表示
- `cmd + right click`: その他アクション表示
- `cmd + f`: ファイル内検索
- `ctrl + v`: 矩形選択
- `ctrl + q`: 左パネルの切り替え
- `cmd + b`: 左パネルの表示/非表示
- `ctrl + h`: 左のタブに移動
- `ctrl + l`: 右のタブに移動

## VSCode Neovim
### ショートカット(for Mac)

## Vim
- `I`: 先頭に移動して編集
- `A`: 末尾に移動して編集
- `w`: 単語移動
- `b`: 単語移動(逆)
- `ctrl + d`: 画面半分移動(下)
- `ctrl + u`: 画面半分移動(上)
- `ctrl + c`: 挿入モード終了
- `:n + enter`: nに該当する行へ遷移
- `ctrl + e`: 末尾に移動して編集

## その他
### Chrome
#### Vimium
前提
Custome key mappingに以下設定

```
# Insert your preferred key mappings here.
map h goBack
map l goForward
map H previousTab
map L nextTab
map i LinkHints.activateMode
map I LinkHints.activateModeToOpenInNewTab
map <c-d> scrollPageDown
map <c-u> scrollPageUp
map <c-h> previousTab
map <c-l> nextTab
```

キーマッピング

- 画面スクロール: j, k
- ページ進む戻る: h, l
- リンクの検索: i (大文字のIで別タブで開く)
- タブの移動: H, L, `ctrl + h`, `ctrl + l`
- ブックマーク検索: b

## 未整理

betterSnapTool
cmd + ctrl + h
cmd + ctrl + l
でウィンドウを左右移動できるようにする

2. Karabiner
https://takezoe.hatenablog.com/entry/2020/07/11/011118

4. dotfiles repoの.vimrcのみリンクする

そしてVSCodeでVim拡張入れる。
以下の対応もする
https://www.kennzo.net/vscode-vim

https://github.com/VSCodeVim/Vim#input-method

`defaults write "Apple Global Domain" com.apple.mouse.scaling 80.0` でマウスカーソル速度も変える
