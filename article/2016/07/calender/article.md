# 学年暦の闇
大学の行事をJSONで返してくれるようなものを作ろうとしていた時に気づいた弊大学の闇を話したいと思います.

## calender ?
PHPを使って学年暦をスクレイピングする[ライブラリ](https://github.com/hrgruri/ritsucal)に行事の検索機能を追加しようとしていました. 検索機能と言っても年･月･日を連想配列で渡すと該当の行事が配列で帰ってくる簡単なものです.  
引数の型が指定できるので`\Hrgruri\Ritsucal\Calendar`型と`array`型を引数にしてメソッドを作りました. 学部の学年暦と今日の日付でテストをするとTypeError. 型が違うというエラー. 該当するクラスを見に行くとあるのは`src/Calender.php`.
<font color=red>Calender.php </font>?  
CalendarではなくCalender. ちなみにCalenderは光沢機のこと.

タイプミス? やってしまったと思い, 置換しようと｢calender｣で検索すると
```php
private $url = 'http://www.ritsumei.ac.jp/profile/info/calender/';
```
までヒットした.

## 大学の間違え
ブラウザで確認したところ  
http://www.ritsumei.ac.jp/profile/info/calender/ は存在しているが,  
http://www.ritsumei.ac.jp/profile/info/calendar/ は存在していない.  

大学側も間違えていた. 学年暦のページが光沢機(calender)になっている.

## 今回の原因
~~そもそも大学側が間違えていたので, 私が間違えたのは大学のせいである. むしろ間違いに合わせているので,私は間違えていない~~

1. 単語の綴り確認もせずに,学年暦のURLに合わせてクラス名を決めてしまっていた.
2. 大学のホームページは正しいと思いんでいた.
3. 補完に頼り過ぎた.


## まとめ
英語の綴りは確かめましょう. Googleで｢学年暦｣と検索して1番上に来るような弊大学のホームページだからといって間違いがないとは思ってはいけない.  
そして<font color=red>弊大学の学年暦は光沢機</font>
