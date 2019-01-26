### 【エラーは友達】<br>Django基礎ハンズオン

1. <div class="django-girls-highlight">管理画面からブログ記事を作る（30分）</div>
2. ブログ記事を画面に表示する（40分）
3. ブログ画面からブログ記事を作る（40分）

+++

### 管理画面からブログ記事を作る

1. ロケットを飛ばす（＝Djangoの設定の確認）
2. 管理画面から記事を作れるようにする

+++

### ロケットを飛ばす

1. プロジェクト作成
2. settings.py編集

+++

### (1)プロジェクト作成

- コマンドラインで以下を入力
	- Windows: `django-admin.exe startproject mysite .`
	- macOS: `django-admin startproject mysite .`
- 「現在のディレクトリに@color[#ff9400](mysiteプロジェクト)を作成」という意味

+++

### （参考）プロジェクトとは

- 「あるウェブサイト向けに設定とアプリケーションを集めたもの」
	- ref: [はじめての Django アプリ作成、その 1](https://docs.djangoproject.com/ja/2.1/intro/tutorial01/)
- プロジェクトを作成すると、manage.pyとプロジェクト名のディレクトリ（と中のファイル）ができる
- nikkieのイメージ：Webアプリの土台

+++

### (2)settings.py編集項目

エディタで@color[#ff9400](mysite/settings.py)を編集する

- タイムゾーン `TIME_ZONE`
- 言語コード `LANGUAGE_CODE`
- 静的ファイルのパス追加 `STATIC_ROOT`
- ホスト設定 `ALLOWED_HOSTS`

+++

### (2)settings.py編集 1/2

- `TIME_ZONE`を検索
	- `TIME_ZONE = 'Asia/Tokyo'`に変更
- `LANGUAGE_CODE`を検索
	- `LANGUAGE_CODE = 'ja'`に変更

+++

### (2)settings.py編集 2/2

- `STATIC_URL`を検索
	- `STATIC_URL = '/static/'`が見つかる
	- その下に`STATIC_ROOT = os.path.join(BASE_DIR, 'static')`という行を追加
- `ALLOWED_HOSTS`を検索
	- `ALLOWED_HOSTS = ['127.0.0.1']` に変更

+++

### ロケットを飛ばす

- コマンドラインから以下を順に実行
	- `python manage.py migrate` (データベースの初期設定)
	- `python manage.py runserver`
- ブラウザで次のページにアクセス
	- http://127.0.0.1:8000/

+++

### Djangoの初期設定完了

<span class="sixty-percent-img">
![ロケットが飛んでいます！](elv_Jan_django_errorfriends/assets/part1/1_rocket.png)
</span>

コマンドラインでCtrlキーとCキーを同時押しするとrunserverは止まります

---

### 管理画面から記事を作れるようにする

1. アプリケーション作成
2. ブログ記事データを保存できるようにする
3. 管理画面の設定をする

+++

### (1)アプリケーション作成

- コマンドラインで以下を実行
	- `python manage.py startapp blog`
	- @color[#ff9400](blogディレクトリ)とその中にいくつかのファイルができる

+++

### （参考）アプリケーションとは

- 「実際に何らかの処理を行う Web アプリケーション」
- 「一つのプロジェクトには複数のアプリケーションを入れられます」
	- ref: [はじめての Django アプリ作成、その 1](https://docs.djangoproject.com/ja/2.1/intro/tutorial01/)
- nikkieのイメージ：Webアプリの機能のまとまり

+++

### (1)アプリケーションを使う設定をする

- エディタでmysite/settings.pyを編集する

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog', # この行を追加
]
```

---

### (2)ブログ記事データを保存できるようにする

1. ブログ記事の **モデル** を作成
2. ブログ記事のモデルをデータベースに反映

+++

### (2-1)ブログ記事のモデルを作成

- 今回はブログアプリケーションを作る
- ブログ記事にはどんな項目が必要？
- ブログ記事のデータを保存できるようにしたい
    - **データベース** に保存する

+++

### ブログ記事の項目 1/2

ここで示すのは一例です。

- 「タイトル」(例：Djangoハンズオンレポート)
- 「本文」（例：2019/01/24に参加してきました。・・・）
- 「作成者」(例：nikkie)

+++

### ブログ記事の項目 2/2

- 「作成日時」(例:2019/01/24 23:00)
- 「公開日時」(例:2019/01/25 8:00)

決めた項目を元に、エディタでblog/@color[#ff9400](models.py)を編集する（次のスライドのようにする）

+++

### blog/models.py

```python
from django.db import models
from django.utils import timezone

class Post(models.Model):
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
            default=timezone.now)
    published_date = models.DateTimeField(
            blank=True, null=True)

    def __str__(self):
        return self.title
```

+++

### （参考）ブログ記事モデル（Postモデル）

Postモデルでの名前 | 意味するもの | 備考
----- | ----- | -----
author | 作成者 |  Djangoが用意したUserモデルと紐づけ
title | ブログタイトル | 200文字以下の文字列
text | ブログ本文 | 大量の文字列（複数行に渡って書ける）

+++

### （参考）ブログ記事モデル（Postモデル）

Postモデルでの名前 | 意味するもの | 備考
----- | ----- | -----
created_date | 作成日 | 日付
published_date | 公開日 | 日付
`__str__`||管理画面での記事の表示方法

+++

### (2-2)ブログ記事のモデルをデータベースに反映

コマンドラインで順次実行（ブログ記事がデータベースに保存できるようにする）

1. `python manage.py makemigrations blog`
2. `python manage.py migrate blog`

+++

### データベースにブログ記事の保存場所を用意した

- @color[#ff9400](Excelの表)をイメージする
- 列は、ブログ記事の項目（先ほど決めた）
- 今後は行を追加していく（1つ1つのブログ記事に対応）

author | title | text | created_date | published_date
----- | ----- | ----- | ----- | -----

+++

author | title | text | created_date | published_date
----- | ----- | ----- | ----- | -----

- models.pyでブログ記事の項目に名前をつけた（「作成者」はauthor）
- models.pyで「入力規則」を設定した（日付しか入れられない）

+++

### （参考）makemigrationsとmigrate

- makemigrations：移行ファイル（マイグレーション）を作成
	- `blog/models.py`を元に、記事データを保存するためのテーブルの定義を作成
- migrate：データベースに変更適用
	- 記事データを保存用のテーブルができる（記事のデータが保存できるようになった）

---

### (3)管理画面の設定をする

1. 管理画面から記事を作れるように設定
2. 管理画面にアクセスするユーザ作成

+++

### (3-1)管理画面から記事を作れるように設定

- エディタでblog/@color[#ff9400](admin.py)を編集し、以下のようにする

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

+++

### (3-2)管理画面にアクセスするユーザ作成

- コマンドラインで`python manage.py createsuperuser`
	- ユーザ名
	- メールアドレス
	- パスワード

+++

### 動作確認：管理画面から記事を作る

- コマンドラインで`python manage.py runserver`
- ブラウザでアクセス http://127.0.0.1:8000/admin/
- 先ほど作ったユーザでログイン（ユーザ名とパスワード）

+++

### 管理画面操作

![ログイン後管理画面](elv_Jan_django_errorfriends/assets/part1/2_admin.png)

+++

### 記事を作る

<span class="sixty-percent-img">
![管理画面から記事を作る](elv_Jan_django_errorfriends/assets/part1/3_add_post.png)
</span>

2つほど作ってみましょう

+++

### 管理画面からブログ記事を作る まとめ

- ロケットを飛ばす（＝Djangoの設定の確認）
	- プロジェクト作成、settings.py編集
- 管理画面から記事を作れるようにする
	- アプリケーション作成
	- models.py、admin.py
