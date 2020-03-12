# 下書き機能の追加

今までは投稿するとすぐに公開されましたが、下書きに保存することができます。

## Draftボタンを作成

ナビゲーションにDraftボタンを追加します。

blog/templates/blog/base.html
```html
<li class="nav-item">
    <a class="nav-link" href="{% url 'post_draft_list' %}">Draft</a>
</li>
```

## 下書きのurlを作成

urlはdrafts/にします。

blog/urls.py
```python
  	path('drafts/', views.DraftListView.as_view(), name='post_draft_list'),
```

## 下書きのViewを作成

下書きのviewを追加します。

blog/views.py
```python
class DraftListView(ListView):
	login_url = '/login/'
	template_name = 'blog/post_draft_list.html'
	model = Post

	def get_queryset(self):
		return Post.objects.filter(published_date__isnull=True).order_by('created_date')
```

## 下書きのテンプレートを作成

post_draft_list.htmlファイルを追加し、下書きのテンプレートを作成します。

blog/templates/blog/post_draft_list.html
```html
{% extends 'blog/base.html' %}

{% block header %}
<div class="site-heading">
  	<h1>Draft</h1>
</div>
{% endblock %}

{% block content %}
	{% for post in post_list %}
	<div class="post-preview">
		<a href="{% url 'post_detail' pk=post.pk %}">
		<h2 class="post-title">
			{{ post.title }}
		</h2>
		</a>
		<p class="post-meta">{{ post.created_date }}</p>
		<p>{{ post.text|truncatechars:200 }}</p>
	</div>
	<hr>
	{% endfor %}
{% endblock %}
```

投稿して、下書きページに投稿した内容が表示されるか確認してみましょう。

draftsページを開くと下書きが表示されます。

http://127.0.0.1:8000/drafts/

