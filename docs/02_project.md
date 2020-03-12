# プロジェクトの作成

## Djangoの仕組み

DjangoはMTVモデルを採用しています。

下記のイニシャルを取ったものです。

* Model(データベースに格納されているデータ)
* Template(テンプレートファイルによって定義されたそれぞれのページのデザイン)
* View(どのページを表示させるかを決定する処理)

![仕組み](../img/django.png)

## 用語説明

* ルーティング(urls.py)
  * URLからどのアプリケーションやビューに処理を渡すかを指定します。
* ビュー(views.py)
  * モデルにデーターベース操作を指示し、テンプレートに表示用のデータを渡します。
* フォーム(forms.py)
  * フォーム画面で入力されたデータを保持します。
* モデル(models.py)
  * データベースと連携します。
* テンプレート(xxx.html)
  * HTMLのテンプレートにビューから受け取ったデータを埋め込み表示します。

## プロジェクト作成

Djangoは1つのプロジェクトと1つ以上のアプリケーションで構築します。

複数のアプリケーションを作成して、互いに依存しないようにすると、管理が楽になります。

![プロジェクト](../img/project.png)

``django-admin startproject``コマンドでプロジェクトを作成します。

```
(myvenv) ~$ django-admin startproject mysite .
```

## 環境設定変更

settings.pyを修正してプロジェクトの設定を変更します。

mysite/settings.py
```python
ALLOWED_HOSTS = ['*']

LANGUAGE_CODE = 'ja'
TIME_ZONE = 'Asia/Tokyo'

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

## データベースのセットアップ

migrateコマンドをすることでデータベースがセットアップされます。

```
(myvenv) ~$ python3 manage.py migrate
```

## Webサーバーを起動する

```
(myvenv) ~$ python3 manage.py runserver
```

URLにアクセスすると、Webページが表示されます。  

http://127.0.0.1:8000/

Webサーバーを停止するには、Ctrl + Cを同時に押すと停止します。

![Django](../img/first.png)
