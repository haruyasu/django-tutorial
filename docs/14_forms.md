# フォームの作成

フォームを作成して、Web上で記事を追加したり、編集したりします。

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
    fields = ('title', 'text',)
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
    path('', views.post_list, name='post_list'),
    path('post/<int:pk>/', views.post_detail, name='post_detail'),
    path('post/new/', views.post_new, name='post_new'),
]
```

## フォームページのViewを作成

viewに追加してテンプレートを指定します。

blog/views.py
```python
from .forms import PostForm

def post_new(request):
  form = PostForm()
  return render(request, 'blog/post_edit.html', {'form': form})
```

## フォームページのテンプレートを作成

post_edit.htmlファイルを追加します。

blog/templates/blog/post_edit.html
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

この時に新しい内容を引数として渡します。

viewのpost_new関数を書き換えます。

blog/views.py
```python
from django.shortcuts import redirect

def post_new(request):
  if request.method == "POST":
    form = PostForm(request.POST)
    if form.is_valid():
      post = form.save(commit=False)
      post.author = request.user
      post.published_date = timezone.now()
      post.save()
      return redirect('post_detail', pk=post.pk)
  else:
    form = PostForm()
  return render(request, 'blog/post_edit.html', {'form': form})
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
    path('', views.post_list, name='post_list'),
    path('post/<int:pk>/', views.post_detail, name='post_detail'),
    path('post/new/', views.post_new, name='post_new'),
    path('post/<int:pk>/edit/', views.post_edit, name='post_edit'), # 追加
]
```

### EditのViewを作成

post_edit関数をviewに追加します。

post_newとの違いは、instance=postとしてインスタンスを渡しています。

blog/views.py
```python
def post_edit(request, pk):
  post = get_object_or_404(Post, pk=pk)
  if request.method == "POST":
    form = PostForm(request.POST, instance=post)
    if form.is_valid():
      post = form.save(commit=False)
      post.author = request.user
      post.published_date = timezone.now()
      post.save()
      return redirect('post_detail', pk=post.pk)
  else:
    form = PostForm(instance=post)
  return render(request, 'blog/post_edit.html', {'form': form})
```

これで、ブログ投稿、編集ができるアプリケーションが完成しました。
