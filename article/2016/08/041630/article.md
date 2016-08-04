`composer create-project`でインストールできるようにして, symfony/consoleを利用してsaoriを使用できるようにしました. あとnamespaceを修正.

## v2.0-devをインストール
`composer create-project hrgruri/saori:v2.0.x-dev blog`で開発途中のv2.0をインストールして始めることができます. 最後の`blog`はディレクトリ名なので別のものに変えても構いません.  

## 使用方法
```sh
composer create-project hrgruri/saori:v2.0.x-dev blog
cd blog
php saori

#初期化
php saori init

#下書きファイルを生成 (いきなりpostを使ってもいい)
php saori draft first_article

#記事の投稿
php saori post first_article

#静的サイトを生成
php saori build
```

現在のところ,init, draft, post, buildが使用できます. `-h`使えば簡単な説明が出ると思うのでそちらを参考に.

`php saori draft`は別に使用しないでいきなり`php saori post`しても利用できるのですが, `draft`を使ったほうがいいかと.


## 今後
`draft`した時にはconfig.jsonが作られず, `post`した時に作られるのですが, これだと`post`した後じゃないとconfig.jsonがさわれない. config.jsonを`draft`でも生成しておき, timestampを`post`した時に追加させようと思います.  
