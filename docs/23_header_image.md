# ヘッダー画像の追加

各投稿ページのヘッダー画像を変更する機能を追加します。

![Header](../img/header.png)

## デフォルト画像の追加

デフォルトで表示する画像を追加します。

blog/static/imgフォルダを作成して、その中にtitle.pngを追加します。

```text
└── blog
    └── static
        └── img
            └── title.png
```

フリー素材を使用して、好きな画像をタイトルに追加しましょう。

https://pixabay.com/

ブログで使用する画像は、著作権に気を付けて下さい。

自分で撮影した画像は問題ありません。

## 画像圧縮

画像のサイズが重いと表示速度に影響が出ますので、下記のサイトを使用して、画像を圧縮してから保存します。

幅：1920px 縦：500px

あまりに大きいサイズの画像は必要ありませんので、画像編集ソフトでトリミングしておきます。

https://imagecompressor.com/ja/

## 画像変更機能追加

投稿画面で画像ファイルを指定して、ヘッダー画像として表示します。

### 画像格納フォルダを作成

ルートディレクトリにimagesフォルダを作成します。

```
/images/
```

### 画像ライブラリをインストール

Pythonの画像処理ライブラリPillowをインストールします。

```
(myvenv) ~$ pip3 install pillow
```

### 設定ファイルを変更

settings.pyを変更して、追加したimagesフォルダを認識するようにします。

settings.py
```python
IMAGE_ROOT = os.path.join(BASE_DIR, 'images')
IMAGE_URL = '/images/'
```

### 画像フォルダをurlsに追加

画像フォルダの場所をurlsに追加して、画像を使用できるようにします。

mysite/urls.py
```python
from django.conf.urls.static import static
from django.conf import settings

urlpatterns += static(settings.IMAGE_URL, document_root=settings.IMAGE_ROOT)
```

### 画像のモデルを追加

画像をアップロードしたいので、モデルに追加します。

ImageFieldを使用します。

upload_toでアップロードする画像の場所を指定します。

blog/models.py
```python
class Post(models.Model):
  author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
  image = models.ImageField(upload_to='images',blank=True, null=True)　# 追加
```

### フィールドを追加

forms.pyにimageフィールドを追加します。

blog/forms.py
```python
class PostForm(forms.ModelForm):
  class Meta:
    model = Post
    fields = ('title', 'text', 'image')　# 追加
```

### 画像のviewを追加

imageをpostのviewに追加します。

request.FILES['image']で画像ファイルを取得することができます。

blog/forms.py
```python
def post_new(request):
  if request.method == "POST":
    form = PostForm(request.POST)
    if form.is_valid():
      post = form.save(commit=False)
      post.image = request.FILES['image']　# 追加

def post_edit(request, pk):
  post = get_object_or_404(Post, pk=pk)
  if request.method == "POST":
    form = PostForm(request.POST, instance=post)
    if form.is_valid():
      post = form.save(commit=False)
      post.image = request.FILES['image']　# 追加
```

### テンプレートを変更

投稿画面で画像を投稿できるようにします。

formにenctype="multipart/form-data"を追加します。

画像をアップロードするにはこの指定が必要になります。

blog/templates/blog/post_edit.html
```html
{% block content %}
  <form method="POST" class="post-form" enctype="multipart/form-data">
    {% csrf_token %}
    {{ form.as_p }}
    <div class="text-right">
      <button type="submit" class="save btn btn-success" role="button">Save</button>
    </div>
  </form>
{% endblock %}
```

詳細画面のヘッダーで画像が表示されるようにします。

CSSでbackground-imageを上書きしています。

blog/templates/blog/post_detail.html
```html
{% if post.image %}
<style>
  header.masthead {
    background-image: url('/{{ post.image.url }}') !important;
  }
</style>
{% endif %}

<p>
  {{ post.text|linebreaksbr }}
</p>
```

## マイグレーション実行

モデルを変更したので、マイグレーションをする必要があります。

```
(myvenv) ~$ python3 manage.py makemigrations
(myvenv) ~$ python3 manage.py migrate
```

## サーバー実行

```
(myvenv) ~$ python3 manage.py runserver
```

投稿画面で画像をアップロードできるようになりました。

画像をアップロードして、ヘッダーの画像が変更されるか確認してみましょう。

