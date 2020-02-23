# 動的データの作成

動的に変わるデータはViewで処理をします。

追加したmodelをインポートしましょう。

今回はPostをインポートします。

そして、クエリセットを作成して、posts変数に代入します。

## クエリとは

データベースからデータを取得するための記述方法です。

## クエリセットとは

クエリの実行結果をクエリセットと呼びます。

公式ドキュメント
https://docs.djangoproject.com/ja/2.2/topics/db/queries/

分かりやすく解説されています。
https://qiita.com/okoppe8/items/66a8747cf179a538355b

blog/views.py
```python
from django.shortcuts import render
from django.utils import timezone
from .models import Post

def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
    return render(request, 'blog/post_list.html', {'posts': posts})
```
renderの最後の引数に{}で囲われたクエリセットを指定します。

この引数の情報がテンプレートが表示することができます。

シングルクォーテーションで囲われたpostsは名前で値がクエリセットのpostsです。

