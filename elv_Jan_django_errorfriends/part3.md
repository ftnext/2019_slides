### 【エラーは友達】Django基礎ハンズオン

1. 管理画面からブログ記事を作る（前半15分）
2. ブログ記事を画面に表示する（前半30分）
3. ブログ画面からブログ記事を作る（後半45分）←

+++

### ブログ画面からブログ記事を作る

- 現状：記事は管理画面から作ることができる
- 管理画面以外からも記事を作れるようにしたい
- ゴール：記事一覧ページ`http://127.0.0.1:8000/`に記事の作成フォームに遷移するリンクを追加。フォームから記事が作成できる
- ※管理画面にログインしているユーザ以外にはリンクを見せない

+++

### ブログ画面からブログ記事を作る

- 基本テンプレート導入
- 記事作成フォーム設定
- フォームに遷移できるようにする
- フォームから保存できるようにする

---

### 基本テンプレート

- 記事作成フォームを表示するために、新規のテンプレートを作ることになる
- どのページにも共通する部分（例：見出しのDjango Girls Blog）はそれぞれのテンプレートで書きたくない
	- 見出しを変えることになったときに苦労する
	- そこで、基本テンプレートに共通化する

+++

### 基本テンプレート base.html

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

- ブログアプリで使うCSSの設定と見出しの部分を共通化
- `{% block content %}` `{% endblock %}`
	- この部分は各テンプレートの内容で置き換わる

+++

### post_list.html アップデート

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
- これまで同様、記事一覧が表示されるが、テンプレートのファイルの構成が変更されている

+++

### 動作確認：ブログ記事を画面に表示する

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで`http://127.0.0.1:8000/`にアクセス

---

### 記事作成フォーム設定

- エディタでblog/forms.pyを作成
- Postモデルをもとにしたフォーム（入力欄の集まり）を作る
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

### blog/forms.py

`class Meta`

- `model = Post`：Postモデルを元にする設定
- `fields`：フォームには記事のタイトルと本文が入力できるようにする

---

### フォームに遷移できるようにする

- 「Django Girls Blog」という見出し部分に、**記事作成フォームへのリンクを追加** する
- 具体的には、プラス(+)アイコンをクリックすると、記事作成フォームに遷移するとする
- エディタでbase.htmlを編集

+++

### base.html 変更箇所

```html
<div class="page-header">
    <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a> <!-- 追加 -->
    <h1><a href="/">Django Girls Blog</a></h1>
</div>
```

+++

### 第3のエラー NoReverseMatch

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで`http://127.0.0.1:8000/`にアクセス
- 記事一覧ページではなく`NoReverseMatch`というエラーが表示される

+++

スクショ

+++

### NoReverseMatchの原因

> Reverse for 'post_new' not found.

- 追加したaタグ `href="{% url 'post_new' %}"`
- 設定された`urlpatterns`から`name='post_new'`と設定されているURLを返す
- 現在`name='post_new'`というURLは設定されていない

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

### NoReverseMatch解消するも

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- AttributeErrorにより、サーバが起動しない

> AttributeError: module 'blog.views' has no attribute 'post_new'

+++

### AttributeErrorの原因

- 先ほどはurlpatternsで設定した`post_list`関数がblog/views.pyの中にないために発生
	- `path('', views.post_list, name='post_list')`
- 直近でurlpatternsで設定した`post_new`関数もまだblog/views.pyの中に用意していない
	- `path('post/new/', views.post_new, name='post_new')`

+++

### ビューを作る（blog/views.pyの`post_new`関数）

- まずは記事作成フォームを**表示**する
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

### AttributeError解消するも

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで`http://127.0.0.1:8000/`にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリックすると、`TemplateDoesNotExist`

+++

スクショ

+++

### TemplateDoesNotExistの原因

- 先ほどは`blog/templates/blog/post_list.html`を作っていなかったために発生
	- `render(request, 'blog/post_list.html', {'posts': posts})`
- 今回も`blog/templates/blog/post_edit.html`を作っていない
	- `render(request, 'blog/post_edit.html', {'form': form})`

+++

### テンプレート blog/post_edit.html 作成

```html
{% extends 'blog/base.html' %}

{% block content %}
    <h1>New post</h1>
    <form method="POST" class="post-form">{% csrf_token %}
        {{ form.as_p }}
        <button type="submit" class="save btn btn-default">Save</button>
    </form>
{% endblock %}
```

+++

### テンプレート blog/post_edit.html

- `{{ form.as_p }}`：フォームに必要な入力欄を表示
- `{% csrf_token %}`：セキュリティ対策（クロスサイトリクエストフォージェリ）
	- このタグをつけ忘れるとエラーが出る（タグをつけることで解決）
- `<form>`にaction属性が指定されていないので、フォームが表示されているページ自身に対して入力されたデータを送信

+++

### 動作確認：フォームに遷移できるようにする

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで`http://127.0.0.1:8000/`にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリックする

+++

スクショ

---

### フォームから保存できるようにする

- 記事作成フォームから記事を保存できるようにする（`post_new`関数の修正）
- 記事作成フォームへのリンクを管理画面でログインしているユーザだけに見せる

+++

### blog/views.py アップデート

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

### `post_new`関数の修正 1/4

`request.method == "POST"`

- 記事作成ページに遷移してきた時、Falseとなる
	- フォームを表示する処理
- フォームが表示されているページ自身に対して入力されたデータを送信した時、Trueとなる
	- 入力内容の検証処理・入力内容の保存処理

+++

### `post_new`関数の修正 2/4

- `form = PostForm(request.POST)`：入力された内容でPostFormを作成
- `form.is_valid()`：入力値の検証
	- 入力値に不備がない場合、Trueとなる（保存処理に進む）
	- 入力値に不備がある場合、Falseとなる（入力値を保ったフォームを再表示する）

+++

### `post_new`関数の修正 3/4

記事の保存処理

- `post = form.save(commit=False)`：入力値を元に記事を作成（まだ保存しない）
- 記事に作成者と公開日が未設定のため設定する
- 未設定の項目がなくなったため、`post.save()`で保存する

+++

### `post_new`関数の修正 4/4

- `return redirect('post_list')`：記事一覧画面を表示する
- 記事を保存したら、記事一覧画面に遷移する
- （記事を保存できなかったら、記事作成画面のまま）

+++

### 動作確認：フォームから保存できるようにする

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで`http://127.0.0.1:8000/`にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリック→記事を作成してみる

+++

入力例スクショ

+++

作成されました（一覧ページスクショ）

+++

### 記事作成フォームへのリンクの表示を修正

- 管理画面でログインしているユーザだけに見せる
- **注**：これはセキュリティ対策としては不十分です（ログインしているユーザだけが記事を**作成**できるようにするべき）

+++

### base.html 変更箇所

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

### base.htmlの変更

`{% if user.is_authenticated %}`

- Pythonのif文のイメージ
- アクセスしたユーザが管理画面でログインしている場合、True
- 管理画面でログインしていないユーザについてはFalse

+++

### 動作確認：記事作成フォームへのリンクの表示

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで`http://127.0.0.1:8000/`にアクセス

+++

### 管理画面でログインしている場合

スクショ追加

+++

### 管理画面でログインしていない場合

スクショ追加
