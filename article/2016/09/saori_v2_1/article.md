saori v2.1.0をリリースしました. v2.0の話をしていなかったのでここでまとめて話します.

## create-projectからインストール
`composer create-project hrgruri/saori-skeleton blog`でインストールができるようになりました. これにより
```sh
mkdir blog
cd blog
composer require hrgruri
```
とかしなくてもよくなった. そもそもインストールなので何度もするようなものじゃないですけどね.

## 使い方の変更
symfony/consoleを使用するように変更しました.
```sh
php saori init
php saori draft article_name
php saori post article_name
php saori build
php -S localhost:8000 -t local
```
このような使い方です. saoriはインストール時に存在していますので, 自分で実行のためのコードを書く必要はないです.

## pageコマンドの追加
利用者が記事以外のページを作成したいときに使うコマンドです.
`php saori page about`とすると`contents/page/about.md`が作られます. ここに色々と書いてビルドすると`/about/index.html`が生成されます.

## httpsのリダイレクト
saori(デフォルトのテーマ)ではhttpでアクセスされた際に, httpsへとリダイレクトするように変更しました.
