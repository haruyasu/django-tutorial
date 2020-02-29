# アプリケーションの拡張

投稿の詳細ページを作成します。

## 詳細ページのリンクを作成

post_list.htmlを変更しましょう。

タイトルのリンクを設定します。

url 'post_detail' pk=post.pkとすることで詳細ページへのリンクを張ることができます。

名前をpost_detailとします。

blog/templates/blog/post_list.html
```html
<a href="{% url 'post_detail' pk=post.pk %}">
  <h2 class="post-title">
    {{ post.title }}
  </h2>
</a>
```

## 詳細ページのURLを作成

URLのパターンを指定します。

blog/urls.py
```python
urlpatterns = [
  path('', views.PostListView.as_view(), name='post_list'),
  path('post/<int:pk>/', views.PostDetailView.as_view(), name='post_detail'),
]
```

## 詳細ページのViewを追加

view.pyにPostDetailViewクラスを追加します。

blog/views.py
```python
from django.views.generic import (ListView, DetailView)


class PostDetailView(DetailView):
  model = Post
  template_name = "blog/post_detail.html"
```

## 詳細ページのテンプレートを追加

post_detail.htmlファイルを追加します。

blog/templates/blog/post_detail.html
```html
{% extends 'blog/base.html' %}

{% block header %}
<div class="post-heading">
  <h1>{{ post.title }}</h1>
  {% if post.published_date %}
    <span class="meta">{{ post.published_date }}</span>
  {% endif %}
</div>
{% endblock %}

{% block content %}
<p>
  {{ post.text|linebreaksbr }}
</p>
{% endblock %}
```

トップページで投稿したタイトルをクリックすると、詳細画面が表示されました。

次は、投稿フォームを作成していきましょう。
