# テンプレートの作成

DjangoはHTMLの中にテンプレート言語という記述を用いて、データベースの値を表示したり、条件分岐やループなどの制御をすることができます。

テンプレートは、templatesというディレクトリに.html拡張子で作成する必要があります。

## 変数を表示

変数を表示するためには、\{\{ 変数名 \}\}を使用します。

## 制御処理

条件分岐やループなどの制御処理は、\{% <タグ名> %\}を使用します。

## デフォルトで使用可能な変数

* user
  * アクセスユーザー情報
* objectまたはモデル名
  * ビューから渡されるモデルオブジェクト
* object_listまたはモデル名_list
  * ビューから渡されるモデルオブジェクトのリスト
* message
  * メッセージリスト
* form
  * フォームオブジェクト

## 組み込みフィルタ

変数にフィルタを使用することができます。

```
{{ var|default:''}}
{{ var|default_if_none:''}}
{{ var|linebreaksbr }}
{{ var|safe }}
{{ var|truncatechars:100 }}
{{ var|urlize }}
```

* default
  * 変数がFalseの場合に表示する値を指定
* default_if_none
  * 変数がNoneの場合に表示する値を指定
* linebreaksbr
  * 改行コード「\n」をHTMLの「<br>」に変換
* safe
  * 自動エスケープを無効化する
* truncatechars
  * 指定した文字数を超えた場合は...と表示する
* urlize
  * URLとメールアドレスをHTMLのアンカータグ「<a>」で表示する

## 組み込みタグ

* autoescape
  * 自動エスケープ機能を制御する
* block
  * 子テンプレートの内容に置き換える
* extends
  * 親テンプレートを拡張することを宣言する
* for, endfor
  * ループする
* if, elif, else, endif
  * 条件分岐する
* load
  * カスタムテンプレートタグを読み込む
* url
  * URLを逆引きする

## form変数オプション

* as_p
  * <p>タグで各フィールドを描画
* as_table
  * テーブル形式で各フィールドを描画
* as_ul
  * リスト形式で各フィールドを描画

## テンプレートを作成

デフォルト値のpost_listを使用して、投稿のリストを表示します。

ListViewを使用した場合、モデル名に「_list」を付けた名前がデフォルトで使用されます。

forと指定することで、post_listのリストをループして一つずつ表示することができます。

blog/templates/blog/post_list.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Django Startup Template</title>
</head>
<body>
  <div>
    <h1><a href="/">Django Startup Template</a></h1>
  </div>

  {% for post in post_list %}
    <div>
      <p>published: {{ post.published_date }}</p>
      <h2><a href="">{{ post.title }}</a></h2>
      <p>{{ post.text|linebreaksbr }}</p>
    </div>
  {% endfor %}
</body>
</html>
```

## 管理画面でPostをPublish

Published dataを追記します。

![Post](../img/publish.png)

## Webサーバー開始

```
(myvenv) ~$ python3 manage.py runserver
```
http://127.0.0.1:8000/

投稿した内容が表示されます。

![Post](../img/hello.png)
