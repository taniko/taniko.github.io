## はじめに
Laravelで特定のクエリパラメータを使ってクエリを組み立てたいときってありませんか? 例えば, 検索なので, `since_id`があれば, セットされている値以降で絞り込んで検索とかです.
```php
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Asset;
use App\Http\Requests\Asset\SearchRequest;

class AssetController extends Controller
{
    public function search(SearchRequest $request)
    {
        $query = Asset::query();
        if ($request->has('since_id')) {
            $query = $query->where('id', '>=', $request->input('since_id'));
        }
        if ($request->has('until_id')) {
            $query = $query->where('id', '<=', $request->input('until_id'));
        }
        return $query->get();
    }
}
```
こんな感じで書けますよね.  
ただ, これだと何個もif文を書いていくことになります. メソッドチェーンでやってみたくなったので, やってみましょう.

## やり方
### マクロの登録
まず, クエリビルダで`if`と`whereIf`を使えるように登録します. `app/Providers/AppServiceProvider.php`に以下のコードを加えます.
```php
<?php
// app/Providers/AppServiceProvider.php
namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Database\Query\Builder;
use Illuminate\Support\Facades\Schema;

class AppServiceProvider extends ServiceProvider
{
    public function boot()
    {
        Builder::macro('if', function (bool $condition, callable $func) {
            return $condition ? $func($this) : $this;
        });
        Builder::macro('whereIf', function (bool $condition, $column, $operator = null, $value = null, $boolean = 'and') {
            return $condition ? $this->where($column, $operator, $value, $boolean) : $this;
        });
    }
}
```

まず1つ目は, コールバック関数を与える方法です. これは, 複雑なクエリを付け加えたい時に使用します. 単純な`where`句を加えたいだけなら, この方法はおすすめしません.  
2つ目は`where`句のみを付属させるものです. `where()`とほぼ同じ使い方なので, こちらがおすすめです. `where()`との違いは, 第1引数が`true`ならば`where`が加えられるという点です.

### 使い方
ユーザの投稿一覧の取得のサンプルコードです.
```php
<?php
// 1つ目 if
$posts = $user->posts()
    ->if($request->has('since_id'), function ($query) use ($request) {
        return $query->where('id', '>=', $request->input('since_id'));
    })->get();

// 2つ目 whereIf
$posts = $user->posts()
    ->whereIf($request->has('since_id'), 'id', '>=', $request->input('since_id'));
```
こんな感じでメソッドチェーンをつなげていくことができます.  
どちらの方が見やすいのか. ブロックで分けるべきか, 1行でまとめるべきか. あと, 型宣言や関数呼び出しの速度も.

## リンク
[Laravel API - https://laravel.com/api/5.5/Illuminate/Database/Eloquent/Builder.html#method_where](https://laravel.com/api/5.5/Illuminate/Database/Eloquent/Builder.html#method_where)
