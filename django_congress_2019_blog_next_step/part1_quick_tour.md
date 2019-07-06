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
2. 作り直しに関わる3トピック

---?color=#ccffcc

@snap[north span-100]
### デモ：ブログアプリでできること
@snapend

@snap[west span-50 text-center]
@ul[](false)

- 公開された記事の一覧
- 公開された記事の詳細
- 記事を作るためにログイン

@ulend
@snapend

@snap[east span-50 text-center]
@ul[](false)

- ドラフト記事を作成
- ドラフト記事を編集・公開
- ※ドラフト記事はログインしないと見えない

@ulend
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

### 作り直しの3トピック

1. プロジェクト作成
2. <span class="omitted-item">名前空間(namespace)</span>
3. settings.pyの分割

[ソースコード tag:1-tutorial_quick_tour](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/1-tutorial_quick_tour)

---

### 作り直しの3トピック

1. **プロジェクト作成**
2. <span class="omitted-item">名前空間(namespace)</span>
3. settings.pyの分割

[ソースコード tag:1-tutorial_quick_tour](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/1-tutorial_quick_tour)

+++

### In Django Girls Tutorial

`django-admin startproject mysite .`

```
djangogirls  # ここでstartproject
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
djangogirls  # ここでstartproject
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

**外側** のmysiteディレクトリを **rename** して使う（ref: 『[Building Django 2.0 Web Application](https://www.amazon.co.jp/dp/B079DW6TRJ)』）

+++

### プロジェクト作成

- Django Girls Tutorialのやり方以外は、あくまで1つのやり方
- 他のプロジェクト作成方法を知っていることで、GitHubのソースコードが読める状態に近づく
  - 例：[PyCon Taiwanのサイト](https://github.com/pycontw/pycon.tw/tree/master/src)  	project: pycontw2016
- 参考：[`django-admin startproject name (directory)`](https://docs.djangoproject.com/en/2.2/ref/django-admin/#startproject)

---

### 作り直しの3トピック

1. プロジェクト作成
2. <span class="omitted-item">名前空間(namespace)</span>
3. **settings.pyの分割**

[ソースコード tag:1-tutorial_quick_tour](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/1-tutorial_quick_tour)

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

[ファイルの差分の参考PR](https://github.com/ftnext/nextstep_djangogirls_tutorial/pull/1/files)

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
- 作り直しに着手。2点共有
  - プロジェクト作成
  - settings.pyの分割

+++?color=#ccffcc

### 初演から省略したトピック

- [名前空間（テンプレート、URL）](https://gitpitch.com/ftnext/2019_slides/master?p=django_congress_2019_blog_next_step#/6)
- [共通テンプレートの配置](https://gitpitch.com/ftnext/2019_slides/master?p=django_congress_2019_blog_next_step#/8/1)

興味がある方は初演スライドをご確認ください
