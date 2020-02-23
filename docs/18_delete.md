# 削除機能の追加

投稿した内容を削除できる機能を追加します。

## 削除ボタンを作成

編集ボタンの下にDeleteボタン追加します。

blog/templates/blog/post_detail.html
```html
<a class="btn btn-danger" href="{% url 'post_remove' pk=post.pk %}" role="button">Delete</a>
```

## 削除ボタンのurlを作成

blog/urls.py
```python
path('post/<pk>/remove/', views.post_remove, name='post_remove'),
```

## 削除ボタンのViewを作成

blog/views.py
```python
def post_remove(request, pk):
  post = get_object_or_404(Post, pk=pk)
  post.delete()
  return redirect('post_list')
```

詳細ページでDeleteボタンを押して、投稿が削除されるか確認しましょう。

削除されたら、トップページに移動します。

これで、投稿、編集、削除機能が実装することができました。

次はセキュリティを強化していきましょう。
