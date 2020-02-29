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
  path('post/<int:pk>/remove/', views.PostDeleteView.as_view(), name='post_remove'),
```

## 削除ボタンのViewを作成

blog/views.py
```python
from django.urls import reverse_lazy
from django.views.generic import (TemplateView, ListView, DetailView, CreateView, UpdateView, DeleteView)


class PostDeleteView(DeleteView):
  model = Post
  template_name = "blog/post_confirm_delete.html"
  success_url = reverse_lazy('post_list')
```

## テンプレートを作成

削除ボタンを押した時の画面を作成します。

post_confirm_delete.htmlファイルを作成します。

blog/templates/blog/post_confirm_delete.html
```html
{% extends 'blog/base.html' %}

{% block header %}
<div class="site-heading">
  <h1>Post Delete</h1>
</div>
{% endblock %}

{% block content %}
<div class="row justify-content-center">
  <form method="post">
    {% csrf_token %}
    <div class="text-center">
      <p>{{ object }}を削除してもよろしいですか？</p>
      <p>
        <button type="submit" class="save btn btn-danger" role="button">Delete</button>
      </p>
    </div>
  </form>
</div>
{% endblock %}
```

詳細ページでDeleteボタンを押して、投稿が削除されるか確認しましょう。

Deleteボタンを押すと削除確認画面に移動します。

削除確認画面でDeleteボタンを押すと、投稿が削除されます。

これで、投稿、編集、削除機能が実装することができました。

次はセキュリティを強化していきましょう。
