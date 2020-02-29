# URLの作成

ルーティングを設定します。

ルーティングはurls.pyに定義します。

ルーティングはプロジェクト用とアプリケーション用が存在します。

## プロジェクト用ルーティング

プロジェクト用ルーティングは、管理サイト用のルーティングになります。

include関数でアプリケーションのurlsに処理をすることを指定します。

## アプリケーション用ルーティング

アプリケーション用のルーティングは、URLとビューのマッチングをします。

このファイルは自動生成されないので、作成する必要があります。

## プロジェクト用ルーティングを作成

トップページにアクセスした時には、blog.urlsへリダイレクトするようにします。

mysite/urls.py
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')), #追加
]
```

## アプリケーション用ルーティングを作成

blogの下に、urls.pyファイルを作成します。

トップページにviewのPostListViewを割り当てます。

トップページにアクセスした時に、PostListViewをみることになります。

as_viewメソッドは、クラスビューをビュー関数化する働きをします。

クラスビューを使用する場合は必須になります。

blog/urls.py
```python
from django.urls import path
from blog import views

urlpatterns = [
    path('', views.PostListView.as_view(), name='post_list'),
]
```

次は、viewのPostListViewを作ります。
