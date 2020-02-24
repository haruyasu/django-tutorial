# セキュリティの強化

ログインしている人だけが投稿、編集、削除、公開をできるように修正します。

各ボタンはログインユーザーだけに表示されるように制限をしましたが、viewの中にも制御する必要があります。

## viewに追記

@login_requiredを追記すると、ログインしている人だけに制限できます。

blog/views.py
```python
from django.contrib.auth.decorators import login_required
```

post_new, post_edit, post_draft_list, post_remove, post_publish関数の上にデコレーターを追記します。

```python
@login_required
def post_new(request):
    [...]
```

ログインしている人だけが投稿、編集、削除、公開をできるようになりました。

次は、ログイン、ログアウト、サインイン機能を追加していきます。
