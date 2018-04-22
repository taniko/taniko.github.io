Laravel 5.6での話です. 5.6から, 新たにモデルを作成した際に`200 OK`ではなく, `201 Created`を返すようになったってだけの話です. (今更?)

## どういうことか

LaravelをAPIとして利用していた時に, Eloquentモデルを返した際に, `200`だったのが, `201`に変更になりました.  
```php
// app/Http/Controllers/PostController.php
<?php

namespace App\Http\Controllers;

use App\Post;
use App\Http\Requests\Post\CreateRequest;

class PostController extends Controller
{
    public function create(CreateRequest $request)
    {
        return $request
            ->user()
            ->posts()
            ->save(Post::make($request->only(['text'])));
    }
}
```
こんな感じのコードがあった場合, 5.5までだと`200 OK`で新規に作成されたPostのデータがレスポンスとして, 返ってきていました. しかし, 5.6からは`201 Created`とPostのデータが返ってくるようになりました.  
特に副作用がなさそうですが, テストやライブラリで`200`かを使っていれば思わぬ動作をしてしまいます. 皆さんは, axiosとかでasync/awaitとかthen/catchとか使っているので大丈夫ですよね. 私はPHPUnitで`assertStatus(200)`とかしていたのでテストが転けた.

地味な変更点ではあるかと思いますが, せっかく`201 Created`という, ちゃんと意味があるものがあるので, 嬉しいですね.

## ちなみに
この話自体はLaravel 5.5の時に出ていて, [PR](https://github.com/laravel/framework/pull/21603)も出されていましたが, バグフィックスとかではなく, 破壊的変更であったため, 見送られ, 5.6で[PR](https://github.com/laravel/framework/pull/21625/)がマージされました. 仕組み自体はRouterでレスポンス(コントローラでreturnしたもの)が`Illuminate\Database\Eloquent\Model`で,`wasRecentlyCreated`が`true`だったら`201 Created`で返すって感じです. 詳しくは[コード](https://github.com/mathieutu/framework/blob/f8af1166169d98a12af54aae8ceff87cea55bbbd/src/Illuminate/Routing/Router.php#L704-L705)を.
