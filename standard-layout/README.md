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

## ポイント

### marginの総裁について

隣接する要素のマージンは相殺される
=> marginが20pxの要素同士が隣接してもその間隔は40pxではなく20oxになる

### floatの解除について

floatプロパティをしようした要素は親要素の高さに影響を与えなくなる
=> clearfixという手法を使用

`clear: both;` を指定することで直前までのfloatが解除され親要素が認識できるようになる

```
<div class="border">
  <div class="left"></div>
  <div class="right"></div>
  <div class="clear"></div>
</div>
<div class="bottom"></div>
```

ただ、毎回余分な要素とスタイルを記述するのは面倒なので
擬似要素を代用できる

```
.border::after {
  content: '';
  display: block;
  clear: both;
}
```

しかし、回り込みを解除したい親要素に毎回この記述をするのは面倒なので
専用のクラスに切り出す

```
.clearfix::after {
  content: '';
  display: block;
  clear: both;
}
```

専用のクラスを追加

```
<div class="border clearfix">
  <div class="left"></div>
  <div class="right"></div>
</div>
<div class="bottom"></div>
```

clearfix以外にも親要素に `overflow: hidden;` または `overflow: auto;` 指定することで
回り込みを解除することもできるが、画面サイズが変わった場合などにはみ出したコンテンツが
見えなくなってしまう可能性があるため注意が必要

### ベースとなるCSSの定義

- 使用するフォントの種類
- テキストの文字色
- ベースとなるフォントサイズ
- リンクの文字色

```
@charset "UTF-8";

html {
  font-size: 62.5%;
}

body {
  color: #333;
  font-size: 1.2rem;
  font-family: "Hiragino Kaku Gothic ProN", Meiryo, sans-serif;
}

*, *::before, *::after {
  box-sizing: border-box;
}

a:link, a:visited, a:hover, a:active {
  color: #d03c56;
  text-decoration: none;
}
```

### remとemの違い

CSS3からremという単位が追加
emは親要素のfont-sizeを1とした倍率を指定
remは[root+em]の名前が示す通り、ルート要素のfont-sizeを1とした倍率を返す

```
<div class="parent">
  親要素のテキスト
  <div class="child">
    子要素のテキスト
  </div>
</div>
```

```
html {
  font-size: 10px;
}

.parent {
  font-size: 1.2em; => 10px(html)*1.2=>12px
}

.child {
  font-size: 1.2em; => 12px(.parent)*1.2=>14.4px
}
```


```
html {
  font-size: 10px;
}

.parent {
  font-size: 1.2rem; => 10px(html)*1.2=>12px
}

.child {
  font-size: 1.2rem; => 12px(html)*1.2=>12px
}
```

remを使用する際は、html要素のfont-sizeは%指定されることが一般的。
主要なブラウザのデフォルトフォントサイズは16pxなので、
62.5%を指定して10pxに相当する。
%指定にしておくことでユーザーがブラウザの設定でデフォルトの文字サイズを変更していた場合にも
ある程度その設定を反映できる

### backgroundプロパティ

backgroundプロパティを使用する際は初期値があるので
background-colorなどと併用する場合は一番最初に書くようにする

### アウトラインを意識する

HTMLでマークアップを行う際にはそのマークアップが表す
アウトラインを意識することで、検索エンジンのクローラーや
スクリーンローダーにもきちんと意味の伝わるHTMLを書くことができる

### a要素でdivを囲む

HTML4まではインライン要素であるa要素でブロックレベル要素であるdiv要素を囲むことは
不適切とされていたが、HTML5からは新しくコンテンツモデルという概念が導入され
a要素は親要素次第でdiv要素を囲むことができる
=> a要素の親要素がdiv要素を囲める要素であれば、a要素もそのルールを引き継いでdiv要素を囲むことができる

a要素のdisplayプロパティのデフォルト値はinlineなので
a要素に高さをもたせたい場合はdisplayプロパティにinline-blockかblockの指定が必要になる


### box-sizingプロパティ

要素の幅と高さの指定がボックスモデルのどのエリアをさすかという決まりを変更できる
初期値はcontent-boxでwidthやheightの値が反映されるのはコンテンツエリアにたいしてで
paddingやborderの領域は含まれない
border-boxにすれば含めることができる

