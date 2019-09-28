# Portfolio Site

## 環境
Wordpress 5.2
PHP 7.1.23
Nodejs 10.15.1
Sage 9.0.9
Sageのインストール方法と設定はこちら
https://roots.io/sage/docs/theme-installation/


## 開発方法

ファイル構成は以下のようになる
```
themes/your-theme-name/   # → Sageのルート
├── app/                  # → テーマPHPファイル関連
│   ├── Controllers/      # → コントローラーファイル
│   ├── admin.php         # → カスタマイズセットアップ
│   ├── filters.php       # → テーマフィルター
│   ├── helpers.php       # → ヘルパーファンクション
│   └── setup.php         # → テーマセットアップ関連
├── composer.json         # → appファイルのオートローダー
├── composer.lock         # → いじらない
├── dist/                 # → いじらない
├── node_modules/         # → いじらない
├── package.json          # → Node.js dependencies and scripts
├── resources/            # → テーマのアセットとテンプレートファイル
│   ├── assets/           # → フロントエンドアセット
│   │   ├── config.json   # → コンパイル後のアセット設定ファイル
│   │   ├── build/        # → WebpackとESLintのコンフィグファイル
│   │   ├── fonts/        # → テーマフォント
│   │   ├── images/       # → テーマイメージ
│   │   ├── scripts/      # → テーマJavaScript
│   │   └── styles/       # → テーマCSS
│   ├── functions.php     # → コンポーザーのオートローダー
│   ├── index.php         # → いじらない
│   ├── screenshot.png    # → テーマのスクリーンショット（管理画面用）
│   ├── style.css         # → テーマのMeta情報
│   └── views/            # → テーマのテンプレート
│       ├── layouts/      # → ベースのレイアウトファイル
│       └── partials/     # → その他レイアウトファイル
└── vendor/               # → いじらない
```
基本的には`resources`以下のファイルを編集する。
開発前に以下のコマンドを入力することで、保存時にCSSとJSの構文チェックとbuildをしてくれるため、なるべく使用してください！
```
$ yarn start
```
個別にbuildしたい場合は
```
$ yarn build
```
localhost:3000でいけるお。

### さっそく開発するお
テンプレートの大枠は`/resources/views/layouts/app.blade.php`なので、共通化したいものはここに入れてください！
念の為、ベタ打ち(2019/09/22 記載)
```
<!doctype html>
<html {!! get_language_attributes() !!}>
  @include('partials.head') →partials/deadを表示するよ
  <body @php body_class() @endphp>
    @php do_action('get_header') @endphp
    @include('partials.header') →partials/deaderを表示するよ
    <div class="wrap container" role="document">
      <div class="content">
        <main class="main">
          @yield('content') →partials/contentを表示するよ
        </main>
        @if (App\display_sidebar())
          <aside class="sidebar">
            @include('partials.sidebar')
          </aside>
        @endif
      </div>
    </div>
    @php do_action('get_footer') @endphp
    @include('partials.footer') →partials/footerを表示するよ
    @php wp_footer() @endphp
  </body>
</html>
```

### todo
・head、header、footer周りのテンプレート作成。

### なかのtodo
・routingの周りを調べる。



## 注意事項
リリース前には以下のコマンドを入力して、CSSとJSをコンパイルしてください！
```
$ yarn build:production
```


## 参考資料

内部がLarabelで記述されているため、テンプレート周り(Railsでいうrender)はこちらをチェック
https://qiita.com/makies/items/2ab24188e7f8482bfddc

画像の設定、JSの設定はこちらをチェック
https://roots.io/sage/docs/theme-development-and-building/
↑routeに応じてJSを発火させることができるらしい

## やれたらやりたい
・オートデプロイ化