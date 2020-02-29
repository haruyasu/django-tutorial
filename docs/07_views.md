# Viewの作成

先程、トップページにアクセスしたときに、viewのPostListViewを指定したので、viewにPostListViewクラスを作成します。

投稿のリストを表示したいので、引数にクラスベース汎用ビューであるListViewを指定します。

## クラスベース汎用ビューとは？

クラスベース汎用ビューはDjangoの強力なテンプレート言語です。

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

## 設定した変数を使用

設定した変数を使用したい場合には、汎用ビューで定義されている関数をオーバーライドします。

get_context_data関数を使用すると、使用したい変数に変えることができます。

普段はデフォルト値を使用して、変更したい時だけ値をオーバーライドします。

独自のテンプレートの名前を使用したい場合は、template_nameをオーバーライドします。

## Viewを作成

blog/views.py
```python
from blog.models import Post
from django.views.generic import (ListView)

class PostListView(ListView):
  model = Post
  template_name = "blog/post_list.html"
```

次は、テンプレートのpost_list.htmlを作成します。
