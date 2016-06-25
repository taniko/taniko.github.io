# ritsucal
ritsucalは立命館大学･大学院の学年暦をスクレイピングするPHPのライブラリです. 前から作っていて[GitHub](https://github.com/hrgruri/ritsucal)にあげていましたが,久しぶりに見るとREADME.mdに変な文字が混ざっていたので,いくつか修正して,そのついでに簡単な使い方を書きます.

## インストール
インストールはcomposerからできます
```sh
composer require hrgruri/ritsucal
```

## 使い方
```php
<?php
require 'vendor/autoload.php';
try {
    $client = new Hrgruri\Ritsucal\Client();
    $calenders = $client->getCalenders();
    var_dump($calenders);
} catch (\Hrgruri\Ritsucal\Exception\UrlException $e) {
    print "Error\n";
}
```
こんな感じでコードを書くと動きます. 得られるのは以下の学年暦.  
1. 2016年度　立命館大学　学年暦

2. 2016年度　立命館大学大学院　学年暦 セメスター制
  （法学研究科、経済学研究科、経営学研究科、社会学研究科、文学研究科、国際関係研究科、政策科学研究科、応用人間科学研究科、言語教育情報研究科、公務研究科、スポーツ健康科学研究科、映像研究科、先端総合学術研究科）

3. 2016年度　立命館大学大学院　学年暦 セメスター制
  （理工学研究科、情報理工学研究科、生命科学研究科、薬学研究科）

4. 2016年度　立命館大学大学院　学年暦 セッション制
（テクノロジー・マネジメント研究科、経営管理研究科）

5. 2016年度　立命館大学大学院　学年暦
  （法務研究科）

var_dump()した結果の一部です
```
array(5) {
  [0]=>
  object(Hrgruri\Ritsucal\Calender)#66 (2) {
    ["title"]=>
    string(40) "2016年度　立命館大学　学年暦"
    ["events"]=>
    array(79) {
      [0]=>
      object(Hrgruri\Ritsucal\Event)#111 (4) {
        ["year"]=>
        int(2016)
        ["month"]=>
        int(4)
        ["day"]=>
        int(1)
        ["title"]=>
        string(27) "前期セメスター開始"
      }
      [1]=>
      object(Hrgruri\Ritsucal\Event)#65 (4) {
        ["year"]=>
        int(2016)
        ["month"]=>
        int(4)
        ["day"]=>
        int(1)
        ["title"]=>
        string(27) "オリエンテーション"
      }
```
デフォルトでは http://www.ritsumei.ac.jp/profile/info/calender/ から情報を取ってきますが,
```php
$calenders = $client->getCalenders('http://www.ritsumei.ac.jp/profile/info/calender/2016/');
```
などのようにすると別の年度の学年暦を取ってくることができます.

***
追記 2016-06-25
## JSON
他の言語でもデータを扱うためにJSON形式で保存する方法です. 
```php
<?php
require 'vendor/autoload.php';
try {
    $client = new Hrgruri\Ritsucal\Client();
    $calenders = $client->getCalenders();
    file_put_contents(
        'file_path',
        json_encode($calenders, JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE)
    );
} catch (\Hrgruri\Ritsucal\Exception\UrlException $e) {
    print "Error\n";
}
```

[file_put_contents()](http://php.net/file_put_contents)で指定したところに保存できます. [json_encode()](http://php.net/json_encode)のJSON_PRETTY_PRINT, JSON_UNESCAPED_UNICODEは見やすい形にしてくれるオプションです.
