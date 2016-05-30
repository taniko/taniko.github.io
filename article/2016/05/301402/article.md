v0.4.0での変更点は
- Twigファイルの場所の変更
- config.jsonの場所を変更
- ユーザページの生成機能

## Twigファイルの場所の変更について
Twigファイルの場所をtheme/:theme_name/twig/にしました. サイトを生成するのに必要なテンプレートはtemplate内に置きました.これからはsaoriが直接呼び出すTwigファイルはここにおいていこうと思います.  

## config.jsonの場所を変更について
contentsディレクトリ内にconfig.jsonを設置するように変更しました. 何故したかというと,config.jsonもgitで管理しやすくするためです.

## ユーザページの生成機能について
それと[前に言ってた](/article/2016/04/261251/),ユーザがMarkdownファイルを作るだけでページを生成できるようにしました. 例えば,contents/page/about.mdというファイルを作るとtemplate/page.twigを利用して,/about/index.htmlが作られます. しかしこれだと画像が扱えない(作ってから気づいた)ので,v0.5では画像をどこかにコピーしてMarkdownファイル内にある画像のパスをそこに書き換えようかな思います.
