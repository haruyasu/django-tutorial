# セキュリティ対策

ブログの投稿、編集はログインしている人だけにできるように変更しましょう。

投稿ボタンや編集ボタンをログインしている人だけに、表示するように制限することができます。

if user.is_authenticatedを使用すると、ログインユーザーだけに制限します。

## Postボタン

blog/templates/blog/base.html
```html
{% if user.is_authenticated %}
  <li class="nav-item">
    <a class="nav-link" href="{% url 'post_new' %}">Post</a>
  </li>
{% endif %}
```

## Editボタン

blog/templates/blog/post_detail.html
```html
{% if user.is_authenticated %}
  <a class="btn btn-success" href="{% url 'post_edit' pk=post.pk %}" role="button">Edit</a>
{% endif %}
```

これでログインユーザーだけに制限できました。
