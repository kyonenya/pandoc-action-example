# pandoc on GitHub Actions

プッシュするだけでマークダウンをWordファイルに変換するワークフロー。

デフォルトでは、mainブランチにプッシュされたとき以下のコマンドが実行され、コンパイル結果が`main_pandoc`ブランチにプッシュされる。

`pandoc [[:digit:]]*.md -o リポジトリ名.docx --reference-doc reference.docx`

## 対象ファイル

数字始まりのmdファイルが昇順で結合されていく。以下のような命名規則を想定している。

- 1_はじめに.md
- 2-1_つぎに.md
- 2-2_さらに.md
- 3_さいごに.md
- README.md（これは除外される）

## reference.docx

テンプレートとなるWordファイル（WordのCSS？）。「スタイル」を指定する。

- 横書きの学術論文を想定
- 40文字30行になるよう設定（フォントサイズ11pt、行間1.1倍）
- 見出し余白は段落前＋段落後でx.5行になるように調整
  - こうすると見出しが入っても行が0.5行分ずれることがない
- pandocが使うスタイル以外は弄らない。
  - 「最良の出力を得るためには、Pandocが利用する下記のスタイルを変更するようにし、それ以外は変更しないようにしてください」[Pandoc User’s Guide 日本語版](https://pandoc-doc-ja.readthedocs.io/ja/latest/users-guide.html#options-affecting-specific-writers)

## 参考にしたサイト

- [(Pandoc) PandocのWordテンプレートはテンプレート出力よりも通常のファイル出力結果を使った方が良い。 - niszetの日記](https://niszet.hatenablog.com/entry/2020/01/03/080000)

## MEMO

- パスパラメータの文字列（`*.md`など）はそのままpandocに渡しても解釈されない。これは、globパターンはまずUnixシェルでファイルリスト（1.md 2-1.md ...）へと展開された後にpandocに渡される仕様であるため。このため、まずパターンをファイルリストに展開して、それを`set-output`コマンドで後のワークフローに持ち越している。
  - [GithubActionsで環境変数を理解する。 - Zenn](https://zenn.dev/hashito/articles/aef4de448f341b)
  - [Concatenate multiple Markdown files using Pandoc on Windows - Stack Overflow](https://stackoverflow.com/questions/49978926/concatenate-multiple-markdown-files-using-pandoc-on-windows)
    - "On Unix-like shells (like bash, for which your script is written) glob expansion (e.g. turning \*.md into file1.md file2.md file3.md) is performed by the shell, not the application you're running."
