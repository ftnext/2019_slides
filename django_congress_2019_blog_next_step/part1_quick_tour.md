### Agenda

- **Django Girls Tutorial クイックツアー**（10min）
- ユーザまわりを実装（10min）
- この機能、どう作る？（10min）
- まとめ（5min）
- 質疑（5min）

+++

### Purpose of Quick Tour

- トークの出発点を合わせる（Django Girls Tutorialを紹介）
- ブログアプリを作り直し始める

+++

### Quick Tour

1. ブログアプリでできることを概観
2. 作り直しに関わる4つのトピックス

---

### ブログアプリでできること

スクリーンショットをもとに紹介します

+++

@snap[west span-50 text-center]
### 公開記事一覧
![だれでも公開記事の一覧が見られます](django_congress_2019_blog_next_step/assets/part1/1_post_list.png)
@snapend

@snap[east span-50 text-center]
### 公開記事詳細
![だれでも公開記事の詳細が見られます](django_congress_2019_blog_next_step/assets/part1/2_post_detail.png)
@snapend

+++

@snap[west span-50 text-center]
### ログイン
![記事を管理するにはログインが必要です](django_congress_2019_blog_next_step/assets/part1/3_login.png)
@snapend

@snap[east span-50 text-center]
### 記事作成
![ログインしたユーザはドラフト記事が作れます](django_congress_2019_blog_next_step/assets/part1/4_new_post.png)
@snapend

+++

@snap[west span-50 text-center]
### ドラフト記事一覧
![ログインしたユーザはドラフト記事の一覧が見られます](django_congress_2019_blog_next_step/assets/part1/5_post_edit.png)
@snapend

@snap[east span-50 text-center]
### 記事の編集
![ログインしたユーザは、ドラフト記事も公開記事も編集できます](django_congress_2019_blog_next_step/assets/part1/6_draft_post_list.png)
@snapend

+++

@snap[west span-50 text-center]
### ドラフト記事の公開
![ログインしたユーザはドラフト記事を公開できます](django_congress_2019_blog_next_step/assets/part1/7_draft_detail.png)
@snapend

@snap[east span-50 text-center]
### 記事の状態
TODO：図を追加
@snapend

+++

### ブログアプリでできること

- だれでも公開記事の一覧、詳細が見られる
- ログインしたユーザはドラフト記事が作成・編集・公開できる
- ログインしたユーザは公開記事が編集できる

+++

### この状態のブログアプリを作るには

- まず、[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)に取り組む
- その後、Extensionsの「[ウェブサイトにもっと機能を追加しよう!](https://tutorial-extensions.djangogirls.org/ja/homework/)」「[ウェブサイトをセキュアにする](https://tutorial-extensions.djangogirls.org/ja/authentication_authorization/)」に取り組む
- それでは、ブログアプリを作り直していきます（※お見せした写真は作り直したブログアプリのものです）

+++

### 作り直しの4トピック

1. プロジェクト作成
2. 名前空間(namespace)
3. 共通テンプレートの配置
4. settings.pyの分割

作り直したポイント全体はこちらをご覧ください

---

### 作り直しの4トピック

1. **プロジェクト作成**
2. 名前空間(namespace)
3. 共通テンプレートの配置
4. settings.pyの分割

+++

### In Django Girls Tutorial

`django-admin startproject mysite .`

```
djangogirls
├── manage.py
├── mysite
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── myvenv  # venv
└── requirements.txt
```

ref: [プロジェクトを作成しよう！](https://tutorial.djangogirls.org/ja/django_start_project/)

+++

### Another way: ディレクトリ込みでプロジェクト作成

`django-admin startproject mysite`

```
djangogirls
├── mysite  # rename to `apps`
│   ├── manage.py
│   └── mysite
│       ├── __init__.py
│       ├── settings.py
│       ├── urls.py
│       └── wsgi.py
├── myvenv
└── requirements.txt
```

**外側** のmysiteディレクトリを **rename** して使う（ref: 『[Building Django 2.0 Web Application](https://www.amazon.co.jp/dp/B079DW6TRJ)）』

+++

### プロジェクト作成

- Django Girls Tutorialのやり方は、1つのやり方にすぎない
- 他のプロジェクト作成方法を知っていることで、GitHubのソースコードが読める状態に近づく
  - 例：[PyCon Taiwanのサイト](https://github.com/pycontw/pycon.tw/tree/master/src)  	project: pycontw2016
- 参考：[`django-admin startproject name (directory)`](https://docs.djangoproject.com/en/2.2/ref/django-admin/#startproject)

---

### 作り直しの4トピック

1. プロジェクト作成
2. **名前空間(namespace)**
3. 共通テンプレートの配置
4. settings.pyの分割

+++

### 名前空間

- テンプレートの名前空間
- URLの名前空間

+++

### テンプレートの名前空間

- `blog/templates/blog/post_list.html` という配置のこと
- アプリのディレクトリ内のtemplatesディレクトリに、**アプリ名（blog）のディレクトリを作ってから**、テンプレートを配置する
- Django Girls Tutorialでは [HTML 入門](https://tutorial.djangogirls.org/ja/html/)

+++

### なぜテンプレートで名前空間を使うのか

- アプリは複数作られるが、アプリ名が一致することはない（`python manage.py startapp app_name`）
- テンプレート名とアプリ名をセットにすることで、**重複しない**
- ref: [はじめての Django アプリ作成、その 3](https://docs.djangoproject.com/ja/2.2/intro/tutorial03/)「テンプレートの名前空間」

+++

### URLの名前空間

- テンプレートと同様に考えて、URLにも名前空間を導入
- blog/urls.pyに`app_name`という変数を定義する

```python
from django.urls import path
from . import views

app_name = 'blog'  # URLの名前空間
urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

+++

### URLの名前空間の使い方

- <app_name>:<path name>（コロンでつなぐ）
- ref: [はじめての Django アプリ作成、その 3](https://docs.djangoproject.com/ja/2.2/intro/tutorial03/)「URL名の名前空間」

----- | -----
`app_name` 導入前 | `{% url 'post_list'}`
`app_name` 導入後 | `{% url 'blog:post_list'}`

+++

### URLの名前空間の使いどころ

- テンプレートのurlタグ `{% url %}`
- ビューのredirectの引数 `redirect('blog:post_list')`
- settings.pyの定数 `LOGIN_REDIRECT_URL = 'blog:post_list'`

---

### 作り直しの4トピック

1. プロジェクト作成
2. 名前空間(namespace)
3. **共通テンプレートの配置**
4. settings.pyの分割

+++

### 共通テンプレート

- Django Girls Tutorial 「[テンプレートを拡張しよう](https://tutorial.djangogirls.org/ja/template_extending/)」
- `blog/templates/blog/post_list.html`と配置しているが、manage.pyと同じ階層にtemplatesフォルダを作り、その中に置く
- blog以外のアプリでも使う意図

```
apps  # = BASE_DIR
├── blog
│   └── templates  # ブログアプリでのみ使うテンプレート
├── manage.py
├── mysite
├── static
│   └── css
└── templates  # 共通テンプレートを置く
    └── base.html
```

+++

### 配置換えに伴って必要な設定変更

- settings.pyのTEMPLATESの[DIRS](https://docs.djangoproject.com/en/2.2/ref/settings/#dirs)
- 各アプリのtemplatesフォルダに加えて、manage.pyと同階層のtemplatesフォルダのテンプレートも使うと設定

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [  # 変更前は空のリスト[]だった
            os.path.join(BASE_DIR, 'templates'),
        ],
        'APP_DIRS': True,
        # 省略
    },
]
```

+++

### 合わせて、CSSも配置換え

- CSSを共通テンプレートで使うので、manage.pyと同階層にstaticディレクトリを作る
- [STATICFILES_DIRS](https://docs.djangoproject.com/en/2.2/ref/settings/#staticfiles-dirs)という変数を定義し、manage.pyと同階層のstaticディレクトリを使う設定

```python
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]
# collectstaticされるディレクトリは、manage.pyと同階層のstaticとは別のディレクトリにする
STATIC_ROOT = os.path.join(BASE_DIR, 'assets')
```

+++

### テンプレートでの呼び出し方

- `{% extends 'base.html' %}` （blog/を前につけなくてよい）
- `{% static 'css/blog.css' %}`

---

### 作り直しの4トピック

1. プロジェクト作成
2. 名前空間(namespace)
3. 共通テンプレートの配置
4. **settings.pyの分割**

+++

### settings.pyの分割

- 冒頭の「settings.pyどこ？」問題を解決するため、自分でsettings.pyを分割してみる
- 手を動かして分割を経験することで、GitHubのソースコードが読める状態に近づく
- ref: @okoppe8 [Django プロジェクト構成のベストプラクティスを探る - ２．設定ファイルを本番用と開発用に分割する](https://qiita.com/okoppe8/items/e60d35f55188c0ab9ecc)

+++

### 分割後のsettings.py

```
mysite  # プロジェクトのディレクトリ
├── __init__.py
├── settings
│   ├── __init__.py
│   ├── base.py  # settings.pyをrename。開発環境、本番環境で共通な設定を残す
│   ├── local.py  # 開発環境向けの設定
│   └── production.py  # 本番環境向けの設定
├── urls.py
└── wsgi.py
```

+++

### 設定の分割例（local.pyの一部）

```python
from .base import (
    INSTALLED_APPS, MIDDLEWARE,
)
from .base import *  # NOQA

DEBUG = True
# django-debug-toolbarの設定
INSTALLED_APPS += [
    'debug_toolbar',
]
MIDDLEWARE += [
    'debug_toolbar.middleware.DebugToolbarMiddleware',
]
INTERNAL_IPS = '127.0.0.1'
```

+++

### 分割に必要な作業 1/2

- base.pyは1階層深いフォルダに配置されたため、`BASE_DIR`変数の定義を更新

```python
BASE_DIR = os.path.dirname(  # -> apps
            os.path.dirname(  # -> mysite（プロジェクトのディレクトリ）
                os.path.dirname(os.path.abspath(__file__))  # -> settings
            )
           )
```

+++

### 分割に必要な作業 2/2

- `DJANGO_SETTINGS_MODULE`の設定を変更
  - manage.py: `mysite.settings.local`
  - wsgi.py: `mysite.settings.production`

```python
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings.local')
```

+++

### 分割の副作用

- 本番環境で`python manage.py ...`する際はsettings引数を指定する
- 例：`python manage.py migrate --settings=mysite.settings.production`

---

### Quick Tour まとめ

- ブログアプリでできることを紹介
- 作り直しに着手。4点共有
  - プロジェクト作成
  - 名前空間(urls.pyの`app_name`)
  - 共通テンプレートの配置(settings.py `TEMPLATES`の`DIRS`)
  - settings.pyの分割
