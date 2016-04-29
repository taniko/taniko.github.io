Saoriにいくつか機能を加えた.
## v0.2
v0.2ではフィード(/feed.atom)を生成するようにしたり,簡単なタグ機能を加えた.
## v0.3
v0.3では機能の追加ではなく,コードを分けたり修正したりした.あと生成する際に使用するtwigファイルの場所を変更したので,v0.2からv0.3でテーマの互換性がないですが,sampleテーマは直した.
## v0.4でしたいこと
v0.4ではconfig.jsonの場所をcontentsの中にしたい. あとinitでconfig.jsonファイルの生成も. 機能としてはテーマが設定したページを作れるようにしたり,ユーザがMarkdownファイルを作るだけで設定されたテンプレートからページを生成できるようにしたい.  
***
現在アクセスできるのは
- /page/:page_number
- /article/:year/:month/:title
- /tag
- /tag/:tag_name/:page_number
