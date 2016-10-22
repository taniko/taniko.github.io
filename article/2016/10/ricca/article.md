[Ricca](https://github.com/hrgruri/ricca)というSlackのフレームワークのようなものをPHPで作りました. できることは少ないですが, なにかメッセージを投げるとそれに一致したコマンドが動いて, Twitterにつぶやかれたり, Slackに文字を返したりするという単純なものです.  
例としては｢tw こんにちは｣とメッセージを送るとTwitterに｢こんにちは｣とつぶやかれるとか｢pid｣でBotの動いているプロセスIDがslackに返ってくとかです.

## コマンドについて
### コマンドの作り方
実際にコードをみてもらうとわかりやすいと思うので[twコマンドのコード](https://github.com/hrgruri/ricca/blob/master/src/Command/Tweet.php)を載せます. configure()で設定をしてexecute()に実際の処理を書くといったものです.
```php
<?php
namespace Hrgruri\Ricca\Command;
class Tweet extends \Hrgruri\Ricca\Command
{
    public function configure()
    {
        $this->setName('tw')
            ->setChannel('general');
    }
    public function execute(\Hrgruri\Ricca\Request $req, \Hrgruri\Ricca\Response $res)
    {
        return $res->withTweet($req->getText())->withText('tweeted');
    }
}
```

### botにコマンドを追加する方法
上記のようなコードを書くだけで簡単にコマンドを作成することができます. 自分で新たにコマンドを作成したら使用できるようにコマンドを追加します. 下のコードはbotを動かすためのコードです. add()で作ったコマンドを登録していけばいいだけです.
```php
<?php
require 'vendor/autoload.php';
$app = new Hrgruri\Ricca\Application(__DIR__.'/data', 'general');
$app->add(new Hrgruri\Ricca\Command\Tweet);
$app->run();
```

---
私のbotのリポジトリ [hrgruri/slack_bot](https://github.com/hrgruri/slack_bot)
