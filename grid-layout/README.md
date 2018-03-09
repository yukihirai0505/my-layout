## HTMLコーディングについて

HTML4=>HTML5になって記述もかなりシンプルになった

- HTML5ではDOCTYPE宣言 => `<!DOCTYPE html>`
- html要素にlang属性を使用して文書の言語を指定することが推奨 => `<html lang="ja">`
- 文字コードはUTF-8を指定することが推奨 => `<meta charset="UTF-8">`

## HTML5の新しい要素

- header => ヘッダー情報
- footer => フッダー情報
- main => メインになるコンテンツ

Internet ExplorerやAndroidの古い機種はmain要素に対応していない
CSSの高さや幅の指定が効かないので対策としては `display: block;` を指定する