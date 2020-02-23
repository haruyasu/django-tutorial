# Viewの作成

先程、トップページにアクセスしたときに、viewのpost_listをみるように指定したので、viewでpost_list関数を作成します。

returnにrender関数をコールして、どのテンプレートファイルを使用するのかを指定します。

こうすることで、url→view→templateの流れを作ることができます。

blog/views.py
```python
from django.shortcuts import render

def post_list(request):
    return render(request, 'blog/post_list.html', {})
```

次は指定した、post_list.htmlを作成することになります。

