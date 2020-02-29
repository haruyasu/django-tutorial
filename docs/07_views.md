# Viewの作成

ビューは、ルーティングからの情報を受け取ってレスポンスの情報を作ります。

## ビューの機能

* フォームに処理を依頼
* モデルにデータベースの操作を依頼
* テンプレートにHTMLの生成を依頼
* 画面遷移先の判断

## ビューの種類

ビューの種類は、クラスベース汎用ビューと関数ベースビューがあります。

## クラスベース汎用ビューとは？

クラスベース汎用ビューは、すでにビューとしての機能を備えていて、継承して使用します。

https://docs.djangoproject.com/ja/2.2/topics/class-based-views/

これを使用すると、記述する量が減り、簡単にViewを作成することができます。

## クラスベース汎用ビューの種類

django.views.genericに、それぞれのビューが準備されているので、importして継承します。

* TemplateView
  * テンプレートを使用して、何かを表示する汎用ビュー
* ListView
  * 一覧を表示する汎用ビュー
* DetailView
  * 詳細ページを表示する汎用ビュー
* CreateView
  * 新しくデータを追加するフォームを提供する汎用ビュー
* UpdateView
  * データを更新するフォームを提供する汎用ビュー
* DeleteView
  * データを削除する汎用ビュー
* RedirectView
  * リダイレクトに特化した汎用ビュー
* FormView
  * フォーム処理をする汎用ビュー

## 設定した変数を使用

設定した変数を使用したい場合には、汎用ビューで定義されている関数をオーバーライドします。

get_context_data関数を使用すると、使用したい変数に変えることができます。

普段はデフォルト値を使用して、変更したい時だけ値をオーバーライドします。

独自のテンプレートの名前を使用したい場合は、template_nameをオーバーライドします。

## オーバーライドするクラス変数

* template_name
  * テンプレート名を指定する
* model
  * モデルを指定する
* paginate_by
  * 1ページに表示する件数を指定する
* queryset
  * テンプレートにクエリセットを渡す
* form_class
  * フォームクラス名を指定する
* success_url
  * 処理成功時にリダイレクトURLを指定する
* fields
  * ビューで使うフォームのフィールドを指定する

## オーバーライドするメソッド

* get_context_data
  * テンプレートに辞書データを渡す
* get_queryset
  * テンプレートにクエリセットを渡す
* form_valid
  * フォームのバリデーションに問題がない場合の処理
* form_invalid
  * フォームのバリデーションに問題があった場合の処理
* get_success_url
  * 処理成功時のリダイレクトURLを指定
* delete
  * 削除処理時の処理を追加
* get
  * 独自のGET通信時の処理を記述
* post
  * 独自のPOS通信時の処理を記述

## 関数ベースビュー

関数ベースビューは、ビューで必要なレスポンスを返すreturn処理まで記述する必要があります。

## Viewを作成

先程、トップページにアクセスしたときに、viewのPostListViewを指定したので、viewにPostListViewクラスを作成します。

投稿のリストを表示したいので、引数にクラスベース汎用ビューであるListViewを指定します。

blog/views.py
```python
from blog.models import Post
from django.views.generic import (ListView)

class PostListView(ListView):
  model = Post
  template_name = "blog/post_list.html"
```

次は、テンプレートのpost_list.htmlを作成します。
