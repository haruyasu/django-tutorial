# モデルの作成

Djangoではモデルをとおして、データベースを構築します。

モデルを使用することで、SQLを意識することなくデータベースを操作することができます。

モデルを定義するにはmodels.pyに追加します。

まずは、投稿機能を作成していきます。

Postモデルを追加します。

クラスを追加し、各プロパティを定義していきます。

ForeignKey、CharField、TextField、DateTimeFieldなどのフィールド解説は公式ドキュメントを参考にして下さい。

https://docs.djangoproject.com/ja/2.2/ref/models/fields/#charfield

## フィールドクラス

* ForeignKey
  * 多対1の関係で他のモデルへのリンク
* CharField
  * 文字列のフィールド
* TextField
  * 多量のテキストのフィールド
* DateTimeField
  * 日付と時刻のフィールド
* IntegerField
  * 整数のフィールド
* FloatField
  * 小数のフィールド

## フィールドオプション

フィールドクラスで使えるオプションです。

* null
  * データベースのNULL可否を設定
* blank
  * フォームフィールドのブランク可否を設定
* choices
  * フォームの選択枠を設定
* default
  * デフォルト値を設定
* unique
  * ユニーク制約を設定
* verbose_name
  * フィールド名を設定
* validators
  * バリデーションの設定

## リレーションフィールドクラス

ForeignKeyを使用すると、モデルクラス間で関連付けをすることができます。

* OneToOneField
  * 1 対 1
* ForeignKey
  * 1 対 多
* ManyToManyField
  * 多 対 多

## on_deleteオプション

* models.CASCADE
  * 一緒に削除される
* models.PROTECT
  * 削除できない
* models.SET_NULL
  * NULLがセットされる
* models.SET_DEFAULT
  * デフォルト値がセットされる
* models.SET
  * 任意の値がセットされる
* DO_NOTHING
  * 何もしない

## モデルを作成

blog/models.py
```python
from django.conf import settings
from django.db import models
from django.utils import timezone
from django.urls import reverse


class Post(models.Model):
  author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
  title = models.CharField(max_length=200)
  text = models.TextField()
  created_date = models.DateTimeField(default=timezone.now)
  published_date = models.DateTimeField(blank=True, null=True)

  def publish(self):
    self.published_date = timezone.now()
    self.save()

  def get_absolute_url(self):
    return reverse("post_detail", kwargs={'pk':self.pk})

  def __str__(self):
    return self.title
```

## データベースにモデルのためのテーブルを作成

モデルを変更したら、下記コマンドで必ずデータベースの再構築が必要になります。

```
(myvenv) ~$ python3 manage.py makemigrations blog
(myvenv) ~$ python3 manage.py migrate blog
```
