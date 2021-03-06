# My HTML5 CSS3 Layout

## コーディングポイント

保守性が高まるポイント

***要素名にスタイルを指定しない***

あとからHTMLのマークアップが変わったときにセレクタを変更するためにCSSも修正しなくてはならない
a,input,textareaなどその要素でないと機能が成り立たない場合は
要素の種類が変わる可能性が低いため、要素名に直接スタイルを指定するデメリットも小さい

***CSSのセレクタにはIDではなくクラスを使用する***

CSSのセレクタにはクラスの他にIDも使用できるが、
IDを避けだ方がいい理由

- スタイルの使い回しができない => 同じページでは1つのIDは複数使用できない
- スタイルの上書きが難しい => CSSには詳細度という概念がある IDはクラスよりも詳細度が高い
- HTMLやJavaScriptと影響範囲を分離する

***リセットCSSについて***

Webサイトを閲覧するユーザーはそれぞれUAシートをもっている
なのでなにもデザインしなくてもある程度見やすい
ただし

- ブラウザごとにUAスタイルシートが異なるためズレが生じる
- UAスタイルシートと独自のデザインが衝突したときいちいち上書きしなければいけない

これらを解消するためリセットCSSがある
normalize.cssはリセット(初期化)ではなくノーマライズ(統一する)という名前の通り
UAスタイルシートの装飾を極力活かしながらブラウザ間の差異のみを埋めていくというアプローチが異なる
UAスタイルシートを活かせそうなサイトデザインであればnormalize.cssもあり

## PART 1

- HTML5の新要素
- アウトライン

http://www.shoeisha.com/book/hp/mcoding/1/

https://github.com/yukihirai0505/my-layout/tree/master/standard-layout/README.md

## PART 2

ブラウザの横幅にあわせてブロックが自動で移動する
可変グリッドレイアウト

- 可変グリッドレイアウトライブラリ
- CSSアニメーション

http://www.shoeisha.com/book/hp/mcoding/2/

https://github.com/yukihirai0505/my-layout/blob/master/grid-layout/README.md

## PART 3

PC/SP両方に対応してシングルページレイアウト

- レスポンスWEBデザイン
- WEBフォント

http://www.shoeisha.com/book/hp/mcoding/3/

https://github.com/yukihirai0505/my-layout/tree/master/singlepage-layout/README.md