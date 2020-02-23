
# 新しいアプリケーションの作成

startappコマンドでアプリケーションを追加できます。

今回はブログを作成するので、名前はblogにします。

```
(myvenv) ~$ python3 manage.py startapp blog
```
```
├── blog
│   ├── admin.py
│   ├── apps.py
│   ├── __init__.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── db.sqlite3
├── manage.py
├── mysite
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── myvenv
│   └── ...
└── requirements.txt
```

### Djangoでアプリケーションを使えるように設定

INSTALLED_APPSに追加します。

mysite/settings.py
```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog.apps.BlogConfig',
]
```

## Djangoの仕組み

DjangoはMTVモデルを採用しています。

下記のイニシャルを取ったものです。

* Model(データベースに格納されているデータ)
* Template(テンプレートファイルによって定義されたそれぞれのページのデザイン)
* View(どのページを表示させるかを決定する処理)


![仕組み](../img/django.png)

最初にモデルを作成していきます。
