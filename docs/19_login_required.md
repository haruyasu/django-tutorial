# セキュリティの強化

ログインしている人だけが投稿、編集、削除、公開をできるように修正します。

各ボタンはログインユーザーだけに表示されるように制限をしましたが、viewの中にも制御する必要があります。

## viewに追記

ログインしている人だけに制限できます。

* 汎用ビューを使用している場合は
  * LoginRequiredMixinを第一引数に指定
* オリジナル関数
  * @login_requiredをデコレーターとして追記

blog/views.py
```python
from django.contrib.auth.decorators import login_required
from django.contrib.auth.mixins import LoginRequiredMixin

class CreatePostView(LoginRequiredMixin, CreateView):
	login_url = '/login/'
	...


class PostUpdateView(LoginRequiredMixin, UpdateView):
	login_url = '/login/'
	...


class DraftListView(LoginRequiredMixin, ListView):
	login_url = '/login/'
	...


class PostDeleteView(LoginRequiredMixin, DeleteView):
	...

@login_required
def post_publish(request, pk):
	...

@login_required
def post_comment(request, pk):
	...
```

ログインしている人だけが投稿、編集、削除、公開をできるようになりました。

次は、ログイン、ログアウト、サインイン機能を追加していきます。
