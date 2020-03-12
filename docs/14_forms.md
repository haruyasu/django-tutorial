# フォームの作成

フォームは、フォーム画面で入力された値をフォームオブジェクトに変換、保持します。

入力値のチェックもおこないます。

https://docs.djangoproject.com/ja/2.2/ref/forms/fields/

## フォームの定義

フォームはdjango.forms.ModelFormクラスを継承して定義します。

django.forms.Formを継承する場合もあります。

## フォームのフィールドクラス

フィールドクラスにはウィジェットが設定されています。

ウィジェットはフィールドのタイプやデザインをまとめたものです。

* CharField
  * TextInput
* IntegerField
  * NumberInput
* ChoiceField
  * Select
* DataField
  * DataInput
* DataTimeField
  * DataTimeInput
* EmailField
  * EmailInput
* FileField
  * ClearableFileInput
* ImageField
  * ClearableFileInput

## バリデーション追加

* validatorsを使用
* clean_<フィールド名>メソッドを使用
* cleanメソッドを使用

## フォームを作成

forms.pyファイルを追加します。

```
blog
   └── forms.py
```

フィールドはタイトルと内容にします。

blog/forms.py
```python
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
	class Meta:
		model = Post
		fields = ('author', 'title', 'text')
```

## フォームページのリンクを作成

Aboutの下にPostリンクを追加します。

blog/templates/blog/base.html
```html
<li class="nav-item">
  	<a class="nav-link" href="{% url 'post_new' %}">Post</a>
</li>
```

## フォームページのURLを作成

post/new/のURLを追加します。

blog/urls.py
```python
urlpatterns = [
  	path('', views.PostListView.as_view(), name='post_list'),
  	path('post/<int:pk>/', views.PostDetailView.as_view(), name='post_detail'),
  	path('post/new/', views.CreatePostView.as_view(), name='post_new'),
]
```

## フォームページのViewを作成

viewに追加してテンプレートを指定します。

blog/views.py
```python
from blog.forms import PostForm
from django.views.generic import (ListView, DetailView, CreateView)

class CreatePostView(CreateView):
	template_name = "blog/post_form.html"
	form_class = PostForm
	model = Post
```

## フォームページのテンプレートを作成

post_form.htmlファイルを追加します。

blog/templates/blog/post_form.html
```html
{% extends 'blog/base.html' %}

{% block header %}
<div class="site-heading">
  	<h1>New post</h1>
</div>
{% endblock %}

{% block content %}
	<form method="POST" class="post-form">
		{% csrf_token %}
		{{ form.as_p }}
		<div class="text-right">
			<button type="submit" class="save btn btn-success" role="button">Save</button>
		</div>
	</form>
{% endblock %}
```

## フォームの保存動作を作成

保存ボタンを押したときに、詳細ページに移動するように修正します。

post_detailにリダイレクトします。

viewのCreatePostView関数を書き換えます。

blog/views.py
```python
class CreatePostView(CreateView):
	template_name = "blog/post_form.html"
	redirect_field_name = 'blog/post_detail.html'
	form_class = PostForm
	model = Post
```

## フォームの編集動作を作成

投稿された内容を編集するボタンを追加します。

### Editボタンを作成

post.textの上にEditボタンを追加します。

blog/templates/blog/post_detail.html
```html
<a class="btn btn-success" href="{% url 'post_edit' pk=post.pk %}" role="button">Edit</a>

<p>
  	{{ post.text|linebreaksbr }}
</p>
```

### Editのリンクを作成

Editボタンを押した後のリンクを追加します。

blog/urls.py
```python
urlpatterns = [
  	...
  	path('post/<int:pk>/edit/', views.PostUpdateView.as_view(), name='post_edit'),
]
```

### EditのViewを作成

post_form関数をviewに追加します。

post_newとの違いは、instance=postとしてインスタンスを渡しています。

blog/views.py
```python
from django.views.generic import (ListView, DetailView, CreateView, UpdateView)


class PostUpdateView(UpdateView):
	template_name = "blog/post_form.html"
	redirect_field_name = 'blog/post_detail.html'
	form_class = PostForm
	model = Post

```

これで、ブログ投稿、編集ができるアプリケーションが完成しました。
