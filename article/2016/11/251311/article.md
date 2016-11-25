v2.2では主にコマンドの追加をしました.
## コマンドの追加
### deploy
`deploy`はデプロイを簡単にするためのものです. git add, commit, pushをまとめてやってくれるといった簡単なものです.
```sh
php saori deploy (:commit_message)
```
これで動作します. `:commit_message`が存在しなければ`date('YmdHi')`が入ります.

### theme
`theme`は存在するテーマ一覧の取得と, テーマの設定ファイルの確認に使います
```sh
php saori theme
## 以下が表示される
Theme list
sample, saori

php saori theme saori
## 以下が表示される
saori/theme.json
{
    "noapp":5,
    "color" : {
        "header" : "#000033",
        "title" : "#EEEEEE",
        "body"      : "#E9E9E9",
        "article"   : "#FFF1CF",
        "main" : "white",
        "side" : "white"
    },
    "date-format" : "Y-m-d"
}
```

## 内部的な話
現在置換え中ですが, PHPの配列から`Illuminate\Support\Collection`に変更中です. Laravelで使われているあれです. まだ書き換えられていないところもあるのですが, 徐々に書き換えていきたいと思います.  
あと, テーマ作成の面で言うと`css.twig`を使えるようにした. これはcss/name.css.twigをcss/name.cssに書き換えると言うもの. theme/saoriではheader, bodyなどの背景色をカスタマイズできるようにするために使用しています.
```css.twig
/* theme/saori/css/article.css.twig */
article {
    background: {{maker.color('article')}};
    margin-bottom: 50px;
    padding: 5px 10px 5px 10px;
}
```
