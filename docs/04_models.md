
# モデルの作成

最初に投稿機能を追加しますので、Postモデルを追加します。

クラスを追加し、各プロパティを定義していきます。

ForeignKey、CharField、TextField、DateTimeFieldなどのフィールド解説は公式ドキュメントを参考にしてみて下さい。

https://docs.djangoproject.com/ja/2.2/ref/models/fields/#charfield

* ForeignKey：多対1の関係で他のモデルへのリンク
* CharField：文字列のフィールド
* TextField：多量のテキストのフィールド
* DateTimeField：日付と時刻のフィールド

分かりやすくまとまっています。

https://qiita.com/nachashin/items/f768f0d437e0042dd4b3

```python
from django.conf import settings
from django.db import models
from django.utils import timezone


class Post(models.Model):
  author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
  title = models.CharField(max_length=200)
  text = models.TextField()
  created_date = models.DateTimeField(default=timezone.now)
  published_date = models.DateTimeField(blank=True, null=True)

  def publish(self):
    self.published_date = timezone.now()
    self.save()

  def __str__(self):
    return self.title
```

## データベースにモデルのためのテーブルを作成

モデルを変更したら、下記コマンドで必ずデータベースの再構築が必要になります。

```
(myvenv) ~$ python3 manage.py makemigrations blog
(myvenv) ~$ python3 manage.py migrate blog
```
