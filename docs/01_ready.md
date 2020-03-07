# 準備

## GitHub

GitHubのアカウントを取得して下さい。

https://github.com/

「New repository」をクリックして、好きな名前でGitHubのリポジトリを作成します。

![GitHub](../img/github.png)

ローカルにリポジトリ名と同じフォルダを作成します。

ローカルフォルダとGitHubのリポジトリを連携します。
```
echo "# django-blog" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/haruyasu/django-blog.git
git push -u origin master
```
※作成したリポジトリ名に変更します。

この時点でREADME.mdだけコミットされていると思います。

### gitignoreファイルを追加

ルートディレクトリに.gitignoreファイルを作成します。

```
django-blog
├── README.md
└───.gitignore
```

記述されたファイルは、git管理下から除外されてコミットされなくなります。

.gitignore
```
myvenv
db.sqlite3
.vscode
__pycache__
*.pyc
```

## 仮想環境

仮想環境を作成します。

### 仮想環境とは

開発を行うときは、用途に応じて専用の実行環境を作成し、切り替えて使用するのが一般的です。

一時的に作成する実行環境を「仮想環境」と言います。

### 仮想環境作成

仮想環境はpythonに標準搭載されている仮想環境プログラムの「venv」を使用します。

ルートディレクトリで下記コマンドを入力します。(django-blogフォルダの中)

```
$ python3 -m venv myvenv
```

コマンドを実行すると、myvenvフォルダが作成されます。

VS Codeを使用している方は、エクスプローラーをリフレッシュすると、フォルダが表示されます。

```
django-blog
├── README.md
├── .gitignore
└───myvenv
```

### 仮想環境実行

sourceコマンドで仮想環境が実行できます。

ルートディレクトリで下記コマンドを入力します。

Linux、Mac
```
$ source myvenv/bin/activate
```

Windows
```
$ .\myvenv\Scripts\activate
```

## 最新pipコマンド

pipコマンドをアップデートしておきましょう。

現在、古いコマンドがインストールされています。

```
(myvenv) ~$ pip3 install --upgrade pip
(myvenv) ~$ pip3 install --upgrade setuptools
```

## 環境準備

環境を準備するのに下記のコマンドを入力してください。

Macの場合
```
(myvenv) ~$ brew install postgresql
```

もしbrewコマンドが認識されない場合は、brewをインストールしてください。

https://brew.sh/index_ja

Linuxの場合
```
sudo apt-get install python3-dev
```

## Djangoパッケージをインストール

requirements.txtを作成し、開発に必要なパッケージをインストールします。

```
django-blog
├── README.md
├── .gitignore
├── myvenv
│   └── ...
└───requirements.txt
```

requirements.txtに各パッケージを記載します。

requirements.txt
```
Django~=2.2
django-heroku==0.3.1
gunicorn==19.9.0
```
※ django-herokuはHerokuにデプロイする時に必要なパッケージです。

pip3 installコマンドでrequirements.txtに記載されたパッケージをインストールします。

```
(myvenv) ~$ pip3 install -r requirements.txt
```

django-herokuをインストールすると、他のパッケージも複数同時にインストールされます。
