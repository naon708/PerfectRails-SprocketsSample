## Sprockets
### SprocketsによるCSSの管理
- `*=`で始まる行はSprocketsが解釈するためのディレクティブ(コメントアウトではない)
- `require_*`での読み込み順に注意
- https://github.com/rails/sprockets#default-directives

### Source Map
- コンパイル前とコンパイル後の対応関係を記したファイル

### 本番向けビルド
```
% bin/rails assets:precompile

# precompile実行後public/assetsディレクトリが作られた
% ls public/assets/
application-xxx.css
application-xxx.css.gz
comments-xxx.css
comments-xxx.css.gz
manifest-xxx.js
manifest-xxx.js.gz
scaffolds-xxx.css
scaffolds-xxx.css.gz
```
- 縮小化などは行われず、Source Mapの宣言が生成されない

```
# assetsファイルの削除
% bin/rails assets:clobber

#=> Removed webpack output path directory /path/to/sprockets_sample/public/packs
```

```
% RAILS_ENV=production bin/rails db:setup
% RAILS_ENV=production bin/rails s
```
- production環境ではpublicディレクトリ以下のファイルは読み込まれない
- そのためnginxなどを用意してpublic配下を配信したりする

```
# 一時的に`public/`をRails自身で配信するように環境変数を指定
% RAILS_SERVE_STATIC_FILES=1 RAILS_ENV=production bin/rails s
```

## rails-ujs
- data属性を利用することでJSの機能を呼び出せる
- HTTPリクエストをAjax化するための機能もある

## Turbolinks
- https://github.com/turbolinks/turbolinks
- https://github.com/turbolinks/turbolinks-rails
