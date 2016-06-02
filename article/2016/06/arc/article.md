# PHPでスクレイピング

創成3では立命館大学アート・リサーチセンター(以下ARC)のアクセスログを使って資料の推薦を行うことが目的でした. 最初はリンクだけを使った質素なものを作る予定でしたが, 途中でスクレイピングをして, サイト内だけで簡単な検索･閲覧をできるようにすることになりました. PHPを使ってやったのですが,これがとっても大変でした.

## 謎のname

HTMLのFormのほとんどにはname属性がつけられています.

```html
<input type="text" name="username">
```
nameからどういった値が入るのか推測できるようになっているべきです.上の例だとユーザ名が入るのだと推測できます. しかしながらARCのフォームでは全くそれがなされていなかった.
### 浮世絵データベース
|name|値|
|:-:|:-:|
|f85|キーワード|
|f23|絵師|
|f83|画題|

### 古典籍データベース
|name|値|
|:-:|:-:|
|f61|資料名|
|f63|編著者|

まったく謎です. ちなみに浮世絵DBの絵師であるf23ですが,古典籍DBでは資料のソート(成立月日順)のために使われています.
ちなみに統一されているものも一応あります.

|name|値|
|:-:|:-:|
|-max|表示件数|
|skip|スキップ数|
この2つは推測できますね. なぜかmaxではなく-maxですが. 統一されておらず,推測できないのはスクレイピングする側としては辛いですね. サーバサイドのコードを書くに扱いづらくなかったのでしょうか?

## 作ったライブラリ
オープンキャンパスのために創成3のサイトを再び作っているので使っているが, それさえ終わればもう使うことはないと思う. [GitHub](https://github.com/hrgruri/rarcs)にアップロードしています. またComposerからインストールして使うことができます.
```sh
composer require hrgruri/rarcs
```

```php
<?php
require 'vendor/autoload.php';

$client = new Hrgruri\Rarcs\NishikieClient();
var_dump($client->getDetail('arcUP2435'));
/*
object(Hrgruri\Rarcs\Asset\Nishikie)#51 (5) {
  ["artist"]=>
  string(6) "広貞"
  ["id"]=>
  string(9) "arcUP2435"
  ["url"]=>
  string(62) "http://www.dh-jac.net/db/nishikie/results-big.php?f1=arcUP2435"
  ["title"]=>
  string(54) "「菅原　三ノ口」「松王丸」「梅王丸」"
  ["cover"]=>
  string(87) "http://www.arc.ritsumei.ac.jp/archive01/theater/image/PB/arc/Prints/arcUP/arcUP2435.jpg"
}
 */
```
