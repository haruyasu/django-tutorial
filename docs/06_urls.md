# URLの作成

各URLを追加するには、urls.pyを編集します。

今回は、トップページのURLを作成します。

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

## blogのURL追加

blogの下に、urls.pyファイルを作成します。

トップページにviewのpost_listを割り当てます。

トップページにアクセスした時に、post_listをみることになります。

blog/urls.py
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

次は、viewのpost_listを作ります。
