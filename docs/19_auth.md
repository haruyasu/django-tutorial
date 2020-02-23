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

## ログイン、ログアウト機能を作成

ログイン、ログアウト機能を実装します。

### ログイン、ログアウトのurlを作成

login、logoutのurlを追記します。

mysite/urls.py
```python
from django.contrib import admin
from django.urls import path, include
from django.contrib.auth import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/login/', views.LoginView.as_view(), name='login'),　# 追加
    path('accounts/logout/', views.LogoutView.as_view(next_page='/'), name='logout'),　# 追加
    path('', include('blog.urls')),
]
```

### テンプレートを追加

blog/templates/registrationフォルダを作成し、login.htmlファイルを作成します。

ログイン画面を作成します。

blog/templates/registration/login.html
```html
{% extends "blog/base.html" %}

{% block header %}
<div class="site-heading">
  <h1>Login</h1>
</div>
{% endblock %}

{% block content %}
  {% if form.errors %}
    <p>ユーザー名、パスワードが間違っています。もう一度入力して下さい。</p>
  {% endif %}
  <div class="row justify-content-center">
    <form method="post" action="{% url 'login' %}">
    {% csrf_token %}
      <table>
      <tr>
        <td>{{ form.username.label_tag }}</td>
        <td>{{ form.username }}</td>
      </tr>
      <tr>
        <td>{{ form.password.label_tag }}</td>
        <td>{{ form.password }}</td>
      </tr>
      </table>
      <div class="text-right">
        <p>
          <button type="submit" class="save btn btn-success" role="button">Send</button>
        </p>
        </div>
      <input type="hidden" name="next" value="{{ next }}" />
    </form>
  </div>
{% endblock %}
```

### 設定を変更

mysite/settings.pyを変更します。

下記のコードを一番下に追加します。

mysite/settings.py
```python
LOGIN_REDIRECT_URL = '/'
```

### テンプレートを変更

baseを修正して、ナビゲーションにLogin、Log outボタンを追加します。

blog/templates/blog/base.html
```html
{% if user.is_authenticated %}
<li class="nav-item">
  <a class="nav-link" href="{% url 'post_new' %}">Post</a>
</li>
<li class="nav-item">
  <a class="nav-link" href="{% url 'post_draft_list' %}">Draft</a>
</li>
<li class="nav-item">
  <a class="nav-link" href="{% url 'logout' %}">Log out</a>
</li>
{% else %}
<li class="nav-item">
  <a class="nav-link" href="{% url 'login' %}">Login</a>
</li>
{% endif %}
```

ログイン、ログアウト機能が実装されました。

ログインして、投稿、編集、削除ボタンが表示されていることを確認してみて下さい。

そして、ログアウトすると、投稿、編集、削除ボタンが表示されません。
