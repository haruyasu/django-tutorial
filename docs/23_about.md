# 固定ページの追加

固定ページを追加します。

自己紹介をするAboutページやコンタクトページなど自由に作成してみて下さい。

ナビゲーションにaboutボタンを追加します。

html:blog/templates/blog/base.html
```html
<li class="nav-item">
  <a class="nav-link" href="{% url 'about' %}">About</a>
</li>
```

## urlを追加

blog/urls.py
```python
  path('about/', views.about, name='about'),
```

## Viewを追加

blog/views.py
```python
def about(request):
  return render(request, 'page/about.html')
```

## テンプレートを追加

/templates/pageフォルダを作成し、about.htmlを追加します。

内容は自由に記載して下さい。

自己紹介を書くといいと思います。

レイアウトを考えて、CSSに追記してみて下さい。
blog/templates/page/about.html
```html
{% extends 'blog/base.html' %}

{% block header %}
<div class="site-heading">
  <h1>About</h1>
</div>
{% endblock %}

{% block content %}
<p>自由に記載して下さい。</p>
{% endblock %}
```

# 完成

ブログアプリケーションの構築が完了です。

記事の投稿、編集、削除、公開、コメント、ログイン、ログアウトなどの機能を操作して、問題がないか確かめて下さい。

問題がなければ、次は全世界に公開します。
