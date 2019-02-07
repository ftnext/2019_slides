### 【羅針盤を手に入れる】<br>Django基礎ハンズオンⅡ

0. ブログアプリの機能のおさらい（10分）
1. ブログ画面からブログ記事を作る（40分）
2. ブログ記事の詳細が見られるようにする（30分）
3. ブログ記事に画像を追加できるようにする（30分）

+++

### ブログ画面からブログ記事を作る

- 前回から参加されている方は復習の時間です
- 今回から初参加の方は一緒に手を動かしましょう

+++

### ブログ画面からブログ記事を作る

- 現状：記事は管理画面から作ることができる
- @color[#ff9400](管理画面以外からも記事を作れる)ようにしたい

+++

### ブログ画面からブログ記事を作る ゴール

- 記事一覧ページ`http://127.0.0.1:8000/`にリンクを追加
- リンクから記事の作成フォームに遷移する
- フォームから記事が作成できる
- ※管理画面にログインしているユーザ以外にはリンクを見せない

+++

### ゴール - 現状

- 記事作成フォーム用のURL、ビュー、テンプレートが必要
- blog/post_list.htmlにフォームへのリンク追加
- 注：リンクを見せない設定はテンプレートでできます

+++

### ブログ画面からブログ記事を作る 手順

1. 記事作成フォーム設定
2. フォームに遷移できるようにする
3. フォームから保存できるようにする
4. ログインしているユーザにだけリンクを見せる

---

### フォーム

- 入力欄の集まり
	- 例：connpassでイベント申し込み。参加コメントを入力
- フォームは入力されたデータを送信する

+++

### (1)記事作成フォーム設定

- エディタでblog/forms.pyを作成
- Postモデルをもとにしたフォームを作る
	- タイトルは200文字以内で入力など、モデルの設定を反映したフォームとなる

+++

### blog/forms.py

```python
from django import forms
from .models import Post

class PostForm(forms.ModelForm):

    class Meta:
        model = Post
        fields = ('title', 'text',)
```

+++

### （参考）blog/forms.py

`class Meta`

- `model = Post`：Postモデルを元にする設定
- `fields`：フォームには@color[#ff9400](記事のタイトルと本文が入力できる)ようにする

---

### (2)フォームに遷移できるようにする

- 「Django Girls Blog」という見出し部分に、@color[#ff9400](記事作成フォームへのリンクを追加)する
- 具体的には、プラス(+)アイコンをクリックすると、記事作成フォームに遷移するとする
- エディタでpost_list.htmlを編集

+++

### post_list.html 変更箇所

```html
<div class="page-header">
    <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a> <!-- 追加 -->
    <h1><a href="/">Django Girls Blog</a></h1>
</div>
```

+++

### 動作確認（一覧画面にリンク追加）

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### NoReverseMatch

記事一覧ページではなく`NoReverseMatch`というエラーが表示される😱

![](elv_Jan_django_errorfriends/assets/part3/1_NoReverseMatch.png)

原因はなんでしょう？（前回からの参加の方向け）

+++

### NoReverseMatchの原因

> Reverse for 'post_new' not found.

- 追加したaタグ `href="{% url 'post_new' %}"`
- `{% url %}`タグは、urls.pyの`urlpatterns`の中から`name='post_new'`と設定されているURLのパスを返す
- 現在`name='post_new'`というURLは@color[#ff9400](設定されていない)

+++

### blog/urls.py

`name='post_new'`というURLを設定する

```python
urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('post/new/', views.post_new, name='post_new'), # 追加
]
```

+++

### NoReverseMatch解消確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### AttributeError

- ブラウザで http://127.0.0.1:8000/ にアクセスできない😱
- コマンドラインを見ると、サーバが起動していない

> AttributeError: module 'blog.views' has no attribute 'post_new'

原因はなんでしょう？（前回からの参加の方向け）

+++

### AttributeErrorの原因

- 原因は、blog/urls.pyの`path('post/new/', views.post_new, name='post_new')`
- blog/@color[#ff9400](views.py)の中に@color[#ff9400](`post_new`関数がない)

+++

### （参考）`path('post/new/', views.post_new, name='post_new')`

引数 | 値 | 意味
----- | ----- | -----
第1引数 | `'post/new/'` | `http://127.0.0.1:8000/post/new/`にアクセスされたら
第2引数 | `views.post_new` | blog/views.pyの`post_new`関数を使って対応する

+++

### ビューを作る（blog/views.pyの`post_new`関数）

- まずは記事作成フォームを@color[#ff9400](表示)する
- ゆくゆくは記事作成フォームから記事を保存したい

+++

### blog/views.py

```python
from django.shortcuts import render
from django.utils import timezone
from .forms import PostForm # 追加
from .models import Post

# post_list関数には変更なし

def post_new(request): # 追加
    form = PostForm()
    return render(request, 'blog/post_edit.html', {'form': form})
```

+++

### `post_new`関数

- blog/forms.pyのPostFormを作成
- PostFormをblog/post_edit.htmlテンプレートに埋め込んで表示

+++

### AttributeError解消確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- 記事作成に進むため、+アイコン（リンク）をクリックする

+++

### TemplateDoesNotExist

+アイコンをクリックした後の画面😱

![](elv_Jan_django_errorfriends/assets/part3/2_TemplateDoesNotExist.png)

原因はなんでしょう？（前回からの参加の方向け）

+++

### TemplateDoesNotExistの原因

> TemplateDoesNotExist: blog/post_edit.html

- 原因：`render(request, 'blog/post_edit.html', {'form': form})`
- テンプレート`blog/post_edit.html`を@color[#ff9400](まだ作っていない)
- テンプレートのファイルを用意する

+++

### テンプレートの空ファイルを用意する

- 作るファイル：`blog/templates/blog/post_list.html`
- 空のファイルを作っただけで、+アイコンをクリックした後にTemplateDoesNotExistは表示されない（ただし真っ白な画面）

+++

### テンプレート blog/post_edit.html の内容

```html
{% load static %}
<html>
    <head>
        <title>Django Girls blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <div class="page-header">
            <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>

        <div class="content container">
            <div class="row">
                <!-- 以下の部分だけが post_list.html と異なる -->
                <div class="col-md-8">
                    <h2>New post</h2>
                    <form method="POST" class="post-form">{% csrf_token %}
                        {{ form.as_p }}
                        <button type="submit" class="save btn btn-default">Save</button>
                    </form>
                </div>
            </div>
        </div>
    </body>
</html>
```

+++

### blog/post_edit.html

- `{{ form.as_p }}`：フォームに必要な入力欄を表示
- `form`はビュー（`post_new`関数）から渡るPostForm

+++

### テンプレートの`<form>`タグ

- method="POST": POSTという方法でデータを送信
- action属性にデータの送信先のパスを指定
  - 指定なし＝@color[#ff9400](フォームのあるページ /post/new 自身に対して)入力されたデータを送信

+++

### （参考）テンプレート blog/post_edit.html

- `{% csrf_token %}`：セキュリティ対策（クロスサイトリクエストフォージェリ）
- このタグをつけ忘れるとエラーが出る（タグをつけることで解決）

+++

### 動作確認：フォームに遷移できるようにする

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- +アイコン（リンク）をクリックする

+++

![フォームに遷移できました](elv_Jan_django_errorfriends/assets/part3/3_display_form.png)

---

### (3)フォームから保存できるようにする

- 「Save」をクリックしても空のフォームが表示される
- /post/new 自身にデータが送信されたときの処理がないため
- `post_new`関数を修正し、記事を保存できるようにする

+++

### `post_new`関数を修正（blog/views.py）

```python
from django.shortcuts import redirect # 追加（他のimportは省略）

# post_list関数には変更なし

def post_new(request):
    if request.method == "POST":
        form = PostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.published_date = timezone.now()
            post.save()
            return redirect('post_list')
    else:
        form = PostForm()
    return render(request, 'blog/post_edit.html', {'form': form})
```

+++

### 修正後の`post_new`関数

- `request.method == "POST"`：データ送信なのか、ページの表示なのかを判断
  - `<form>`タグの設定により、データはPOSTという方法で送信される
- データ送信の場合、入力値に不備がなければ、記事を保存し、記事一覧画面を表示

+++

### （参考）`post_new`関数 1/4

`request.method == "POST"`

条件 | 条件式の値 | 後続処理
----- | ----- | -----
記事作成ページに遷移 | False | フォーム表示
記事作成ページに入力されたデータを送信 | True | 入力内容の検証／保存

+++

### （参考）`post_new`関数 2/4

- `form = PostForm(request.POST)`：入力された内容でPostFormを作成
- `form.is_valid()`：入力値の検証
	- @color[#ff9400](入力値に不備がない場合)、Trueとなる（@color[#ff9400](保存処理)に進む）
	- 入力値に不備がある場合、Falseとなる（入力値を保ったフォームを再表示する）

+++

### （参考）`post_new`関数 3/4

記事の保存処理

- `post = form.save(commit=False)`：入力値を元に記事を作成（まだ保存しない）
- 記事に作成者と公開日が未設定のため設定する
- 未設定の項目がなくなったため、`post.save()`で保存する

+++

### （参考）`post_new`関数の修正 4/4

- `return redirect('post_list')`：記事一覧画面を表示する
- 記事を保存したら、記事一覧画面に遷移する
- （記事に不備があり保存できなかったら、記事作成画面のまま）

+++

### 動作確認：フォームから保存できるようにする

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- +アイコン（リンク）をクリック→記事を作成してみる
- TODO；管理画面でのログインしていない場合にエラーになるか要確認

+++

![フォームから記事を作成](elv_Jan_django_errorfriends/assets/part3/4_post_from_form.png)

+++

### 作成されました

<span class="sixty-percent-img">
![一覧ページに遷移](elv_Jan_django_errorfriends/assets/part3/5_post_created_from_form.png)
</span>

---

### (4)ログインしているユーザにだけリンクを見せる

- +アイコンを管理画面で@color[#ff9400](ログインしているユーザだけ)に見せる
- **注**：これはセキュリティ対策としては不十分です（ログインしているユーザだけが記事を**作成**できるようにするべき）
- 前回カットした部分です。全員で一緒に手を動かしましょう

+++

### post_list.html, post_edit.html 変更箇所

```html
<div class="page-header">
    <!-- 変更箇所 -->
    {% if user.is_authenticated %}
        <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
    {% endif %}
    <!-- 変更箇所 終わり -->
    <h1><a href="/">Django Girls Blog</a></h1>
</div>
```

+++

### 動作確認：記事作成フォームへのリンクの表示

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### 管理画面でログインしている場合

![+リンクが表示される](elv_Jan_django_errorfriends/assets/part3/6_logged_in.png)

管理画面 http://127.0.0.1:8000/admin/

+++

### 管理画面でログインしていない場合

![+リンクが表示されない](elv_Jan_django_errorfriends/assets/part3/7_not_logged_in.png)

+++

### 懸念事項：保守性

- 2つのテンプレートを書き換えた
- テンプレートが増えると修正箇所が増える😫
- post_list.htmlとpost_edit.htmlには共通部分が多い

+++

### 基本テンプレート

- 共通部分を基本テンプレートにまとめる
- 保守性が向上する（基本テンプレートの見出しを変えるだけで済む）
- `blog/templates/blog/base.html`を作成

+++

### 基本テンプレート base.html 作り方

- `blog/templates/blog/post_list.html`をコピー（複製）して`blog/templates/blog/base.html`とする
- `<div class="col-md-8">`を以下のように書き換え

```html
<div class="col-md-8">
    {% block content %}
    {% endblock %}
</div>
```

### 基本テンプレート base.html 全容

前のスライドの手順でうまく動かない場合は、以下をコピーして作成

```html
{% load static %}
<html>
    <head>
        <title>Django Girls blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <div class="page-header">
            {% if user.is_authenticated %}
                <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
            {% endif %}
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>

        <div class="content container">
            <div class="row">
                <div class="col-md-8">
                    {% block content %}
                    {% endblock %}
                </div>
            </div>
        </div>
    </body>
</html>
```

+++

### base.html

- headタグ（ブログアプリで使うCSSの設定）と見出しの部分を共通化
- `{% block content %}` `{% endblock %}`
	- この部分は各テンプレートの内容で置き換わる

+++

### post_list.html アップデート

まるまる以下のように書き換え

```html
{% extends 'blog/base.html' %}

{% block content %}
    {% for post in posts %}
        <div class="post">
            <div class="date">
                <p>published: {{ post.published_date }}</p>
            </div>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaksbr }}</p>
        </div>
    {% endfor %}
{% endblock %}
```

+++

### post_list.html アップデート

- 1行目`{% extends 'blog/base.html' %}`：基本テンプレートblog/base.htmlを使うと設定
- `{% block content %}`〜`{% endblock %}`：blog/base.htmlの`{% block content %}` `{% endblock %}`の部分を置き換える

+++

### 動作確認：ブログ記事を画面に表示する

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス
- テンプレートのファイルを変更したが、これまで同様、記事一覧が表示される

+++

### post_edit.html アップデート

まるまる以下のように書き換え

```html
{% extends 'blog/base.html' %}

{% block content %}
    <h2>New post</h2>
    <form method="POST" class="post-form">{% csrf_token %}
        {{ form.as_p }}
        <button type="submit" class="save btn btn-default">Save</button>
    </form>
{% endblock %}
```

+++

### 動作確認：フォームの表示

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリック → これまで同様、フォームが表示される

+++

### まとめ：ブログ画面からブログ記事を作る

- 3つのエラーを解決しながら、フォームを表示できるようにした
  - NoReverseMatch
  - AttributeError
  - TemplateDoesNotExist

+++

### フォーム表示の手順

1. 既存テンプレートにリンクを追加（NoReverseMatch発生）
2. URLの設定（AttributeError発生）
3. ビューの作成（TemplateDoesNotExist発生）
4. 新規テンプレート作成

+++

### 羅針盤

図

+++

### Django開発という旅路

- 手には羅針盤
- 旅の仲間はエラー
- 一緒に手を動かして進みましょう
