Saoriのバージョン3をリリースしました. 実際にリリースしたのは5月とかなり前です.  
v3での主な変更点は以下のとおりです.
- github.io以外で使用可能
- 設定ファイルをJSONからYAMLに変更
- テーマを外部から追加可能

まず, github.io以外で使用可能になったので, 自分のVPSなどでブログを公開できるようになりました. `config/env.yml`の`public`にURLを記述します.  

設定ファイルをYAMLに変えたのは, JSONの記述が辛かったからです. 括弧とかめんどくさかったのです.

テーマを外部から追加可能というのは, テーマを追加できるようにしたということ(?). コードを見たほうが早い.
```php
<?php
require __DIR__.'/vendor/autoload.php';
$app = new Taniko\Saori\Application(__DIR__);
$app->addTheme('theme-name', __DIR__ . '/theme/append-theme');
$app->run();
```
今までだと[taniko/saori](https://github.com/taniko/saori)に存在するテーマしか使用できなかったのですが, このような感じでテーマを追加して, それを使用できるようにしました.

やっぱり, PHPは最高ですね!
