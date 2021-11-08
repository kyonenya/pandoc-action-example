pandoc \*.md -o result.docx --reference-doc reference.docx

> まずは倍数を試そう。
> 固定値の調整は設定が面倒なので、上下に空いてしまうフォントでない場合は、倍数を選択し 1 ～ 1.2 倍を選択すると楽です。Word のデフォルトである 1.15 倍が基本です
> https://xn--w8yz0bc56a.com/line-space/

> 最良の出力を得るためには、Pandoc が利用する下記のスタイルを変更するようにし、それ以外は変更しないようにしてください:
> https://pandoc-doc-ja.readthedocs.io/ja/latest/users-guide.html#options-affecting-specific-writers

> On Unix-like shells (like bash, for which your script is written) glob expansion (e.g. turning \*.md into file1.md file2.md file3.md) is performed by the shell, not the application you're running. Your application sees the final list of files, not the wildcard.
> https://stackoverflow.com/questions/49978926/concatenate-multiple-markdown-files-using-pandoc-on-windows
