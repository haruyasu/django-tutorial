# テンプレートの作成

Djangoではテンプレートが使用できます。

二重括弧\{\{\}\}で囲うことによって、viewsのreturnの最後の引数で指定した値を使用することができます。

今回の場合はpostsです。

forと指定することで、ループを使うことができます。

postsのリストをループして一つずつ表示します。

blog/templates/blog/post_list.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Django Startup Template</title>
</head>
<body>
  <div>
    <h1><a href="/">Django Startup Template</a></h1>
  </div>

  {% for post in posts %}
    <div>
      <p>published: {{ post.published_date }}</p>
      <h2><a href="">{{ post.title }}</a></h2>
      <p>{{ post.text|linebreaksbr }}</p>
    </div>
  {% endfor %}
</body>
</html>
```

## 管理画面でPostをPublish

Published dataを追記します。

![Post](../img/publish.png)

## Webサーバー開始

```
(myvenv) ~$ python3 manage.py runserver
```
http://127.0.0.1:8000/

投稿した内容が表示されます。

![Post](../img/hello.png)
