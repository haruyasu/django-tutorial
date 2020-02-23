# HTMLの作成

先程、viewでpost_list.htmlを表示するように指定したので、post_list.htmlを作成していきます。

blogの下にtemplatesフォルダとblogフォルダを追加します。

```
blog
└───templates
    └───blog
```

作成したblogフォルダにpost_list.htmlファイルを追加します。

まずは最小限のHTMLを追加してみましょう。

blog/templates/blog/post_list.html
```html
<html>
<body>
    <p>Hello!</p>
    <p>This is working.</p>
</body>
</html>
```

### Webサーバー開始

```
(myvenv) ~$ python3 manage.py runserver
```
http://127.0.0.1:8000/

トップページに文字が表示されましたでしょうか！

Hello!

This is working.
