
# CSSの作成

staticフォルダ、cssフォルダを作成し、blog.cssファイルを作成します。

```
└── blog
    └── static
        └── css
            └── blog.css
```

今回は、下記のテンプレートを使用してブログを作成していきます。

https://startbootstrap.com/themes/clean-blog/

CSSの内容は、githubの内容をコピーして貼り付けておいて下さい。

blog/static/css/blog.css

https://github.com/haruyasu/django-template-upgrade/blob/master/blog/static/css/blog.css

## トップページを変更

Bootstrapを使用して、トップページを変更してみましょう。

Bootstrapの詳しい内容は公式ドキュメントを参考にして下さい。

https://getbootstrap.com/

blog.cssはstatic 'css/blog.css'を指定することで読み込むことができます。

blog/templates/blog/post_list.html
```html
{% load static %}
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta name="description" content="">
  <meta name="author" content="">
  <title>Blog - Django Startup</title>
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.1/css/all.min.css">
  <link rel="stylesheet" href="{% static 'css/blog.css' %}" />
</head>

<body>
  <!-- Navigation -->
  <nav class="navbar navbar-expand-lg navbar-light fixed-top" id="mainNav">
    <div class="container">
      <a class="navbar-brand" href="/">Blog</a>
      <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse"
        data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false"
        aria-label="Toggle navigation">
        Menu
        <i class="fas fa-bars"></i>
      </button>
      <div class="collapse navbar-collapse" id="navbarResponsive">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <a class="nav-link" href="/">Home</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <!-- Page Header -->
  <header class="masthead">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="site-heading">
            <h1>Django Startup</h1>
            <span class="subheading">This is your first step!</span>
          </div>
        </div>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-10 mx-auto">
        {% for post in post_list %}
        <div class="post-preview">
          <h2 class="post-title">
            {{ post.title }}
          </h2>
          <p class="post-meta">{{ post.published_date }}</p>
          <p>{{ post.text|linebreaksbr|truncatechars:100 }}</p>
        </div>
        <hr>
        {% endfor %}
      </div>
    </div>
  </div>

  <hr>

  <!-- Footer -->
  <footer>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <ul class="list-inline text-center">
            <li class="list-inline-item">
              <a href="#">
                <span class="fa-stack fa-lg">
                  <i class="fas fa-circle fa-stack-2x"></i>
                  <i class="fab fa-github fa-stack-1x fa-inverse"></i>
                </span>
              </a>
            </li>
            <li class="list-inline-item">
              <a href="#">
                <span class="fa-stack fa-lg">
                  <i class="fas fa-circle fa-stack-2x"></i>
                  <i class="fab fa-twitter fa-stack-1x fa-inverse"></i>
                </span>
              </a>
            </li>
            <li class="list-inline-item">
              <a href="#">
                <span class="fa-stack fa-lg">
                  <i class="fas fa-circle fa-stack-2x"></i>
                  <i class="fab fa-instagram fa-stack-1x fa-inverse"></i>
                </span>
              </a>
            </li>
          </ul>
          <p class="copyright text-muted">Copyright &copy; Your Website 2020</p>
        </div>
      </div>
    </div>
  </footer>
</body>
</html>
```

Webサイトを更新すると、CSSが反映されています。

一気にブログになったと思います。
