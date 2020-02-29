# 動的データの作成

動的に変わるデータはViewで処理をします。

そして、get_queryset関数の中で、クエリをセットします。

## クエリとは

データベースからデータを取得するための記述方法です。

## クエリセットとは

クエリの実行結果をクエリセットと呼びます。

公式ドキュメント
https://docs.djangoproject.com/ja/2.2/topics/db/queries/

blog/views.py
```python
from django.utils import timezone
from blog.models import Post
from django.views.generic import (ListView)


class PostListView(ListView):
  model = Post
  template_name = "blog/post_list.html"

  def get_queryset(self):
    return Post.objects.filter(published_date__lte=timezone.now()).order_by('-published_date')
```

ここでは、filter関数を使用して、公開順に投稿を並べるように指定しています。
