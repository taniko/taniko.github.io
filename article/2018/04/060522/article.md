注意 - 皮肉的な記事です. いくつか使っていて, 辛いところを記述するので, ネタみたいな記事です.

## 配列周り
PHPには, 配列がありまして, `$foo = [1, 2, 3]`とかです. 前までは`$foo = array(1, 2, 3)`でした.  
そんな配列なのですが, JavaScriptとかRubyとかと違って, arrayであって, array objectではないわけです. そんなわけで, 配列の操作がしたければ, `array_*()`を使うわけです. `array_push()`に関しては, `$array[] = $val`でできます.  
そんなPHPの配列で面白いところは, `array_map()`です. `array_push($array, $val_1)`, `array_filter($array, $callback)`, `array_reduce($array, $callback)`など, 第1引数に配列を持ちます. しかし, `array_map()`は`array_map($callback, $array)`と順番が逆なのです. これが辛い. 統一していて欲しい.  
PHPの配列が辛い人は, `Illuminate\Support\Collection`を使ってオブジェクトにすればいいと思うので, `composer install illuminate/support`しましょう.

## オブジェクトのコピー
PHPのオブジェクトを別の変数に渡す時, `clone`を利用します.

```
<?php
class Sample {
    public $count = 0;
}

$foo = new Sample();
$bar = clone $foo;

$bar->count++;

var_dump($foo->count); // int(0)
var_dump($bar->count); // int(1)
```

もしも`clone`を使用しないと, 思わぬ副作用を生み出します.

```php
<?php
class Sample {
    public $count = 0;
}

$foo = new Sample();
$bar = $foo;

$bar->count++;

var_dump($foo->count); // int(1)
var_dump($bar->count); // int(1)
```

`$foo->count`も書き換わってしまうんですね. そんな`clone`ですが, クローンが作成される際に呼ばれるマジックメソッド`__clone()`というものがあります. これは作成された新たなオブジェクトで呼ばれます.

```php
<?php
class Sample {
    public $count = 0;

    public function __clone() {
        $this->count++;
    }
}

$foo = new Sample();
$bar = clone $foo;

var_dump($foo->count); // int(0)
var_dump($bar->count); // int(1)
```
これにより, 遺伝子操作されたクローンを作ることができます. 使う機会があるかはわかりませんが.

## ついでに
homebrewでのPHPのインストール方法が変わりました. いままでは`brew install php72`だったのですが, これからは, `brew install php@7.2`という形になります. あと, xdebugがインストールされていないようなので, 調べたらpeclを使ってとあったので, `pecl install xdebug`をしましょう. 詳しくは GitHubのIssueで [https://github.com/Homebrew/homebrew-php/issues/4721](https://github.com/Homebrew/homebrew-php/issues/4721)
