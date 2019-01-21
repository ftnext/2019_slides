### 【エラーは友達】Django基礎ハンズオン

1. 管理画面からブログ記事を作る（30分）
2. ブログ記事を画面に表示する（45分）←
3. ブログ画面からブログ記事を作る（可能な範囲で）

+++

### ブログ記事を画面に表示する

- 現状：管理画面で作った記事を管理画面で一覧が見られる
- 管理画面以外でも一覧の記事を確認できるようにしたい
- ゴール：`http://127.0.0.1:8000/`にブラウザでアクセスすると記事の一覧が見られる

+++

### ブログ記事を画面に表示する

1. URLの設定
2. ビューの設定
3. テンプレートに表示
4. CSS導入

---

### (1)URLの設定

- URLとは、Web上の住所
- インターネットの全てのページは独自のURLを持つ
- ブラウザは入力されたURLのページを表示する

+++

### (1)URLの設定

- 記事一覧ページのURLを`http://127.0.0.1:8000/`にする
- 2つのurls.pyをエディタで編集する
	- プロジェクトのurls.py（mysite/urls.py）
	- blogアプリケーションのurls.py（blog/urls.py）**@color[#ff9400](新規作成)**

+++

### mysite/urls.py

2箇所変更する

```python
from django.contrib import admin
from django.urls import path, include # includeを追加

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')), # 追加
]
```

+++

### mysite/urls.pyの大まかな内容

前提：`http://127.0.0.1:8000/`というURLはブログアプリへのアクセス

URL | 設定内容
----- | -----
`http://127.0.0.1:8000/admin/` | 管理画面を表示
`http://127.0.0.1:8000/admin/`以外 | blog/urls.pyの設定を使う

+++

### blog/urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

+++

### blog/urls.pyの大まかな内容

- `http://127.0.0.1:8000/`とブログアプリに<br>アクセスされた場合を設定している
- 現在、`http://127.0.0.1:8000/admin/`と`http://127.0.0.1:8000/`以外のURLでの<br>アクセスは想定していない

+++

### 第1のエラー：AttributeError

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- AttributeErrorにより、サーバが起動しない（ブラウザで http://127.0.0.1:8000/ が開けない）

> AttributeError: module 'blog.views' has no attribute 'post_list'

---

### AttributeErrorの原因

- blog/views.pyの中に`post_list`関数がない
- `path('', views.post_list, name='post_list')`
	- 第1引数：`http://127.0.0.1:8000/`にアクセスされたら
	- 第2引数：blog/views.pyの`post_list`関数を使って対応する と設定した
	- （`post_list`関数には記事一覧を表示する処理を書く）

+++

### (2)ビューとテンプレート

- blog/views.pyに`post_list`関数で記事一覧を表示したい
- Djangoにおける役割分担：ビューとテンプレート（他にモデル）
	- 記事一覧用のデータの取得：ビューが担う（≒ Pythonの関数）
	- 記事一覧の表示：テンプレートが担う（≒ HTMLファイル）

+++

### `post_list`関数の行う処理

1. 記事の一覧をモデルから取得
2. 取得した記事のデータをテンプレートに渡す
3. テンプレートに記事のデータを埋め込んで表示する

+++

### blog/views.py

```python
from django.shortcuts import render
from django.utils import timezone
from .models import Post

def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('-published_date') # 1にあたる
    return render(request, 'blog/post_list.html', {'posts': posts}) # 2と3にあたる
```

+++

### （参考）`post_list`関数 1/2

- `Post.objects.filter(`<br>`    published_date__lte=timezone.now())`
	- 公開日が現在時刻よりも前の記事の一覧を取得
	- （このブログアプリは公開日を未来に<br>設定することもできる）
- `.order_by('-published_date')`
	- 公開日が現在時刻よりも前の記事の一覧を<br>公開日が大きいものが先に来るように並び替え
	- 公開日が大きいものが先＝**最近公開されたものが先**

+++

### （参考）`post_list`関数 2/2

- `render(request, 'blog/post_list.html', {'posts': posts})`
	- `posts`は記事を並べたもの（最近公開されたものが先）
	- `posts`をテンプレート`blog/post_list.html`に渡す
	- `blog/post_list.html`に`posts`のデータを埋め込んで表示する

+++

### 第2のエラー：TemplateDoesNotExist

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス
- 記事一覧ページと思いきや`TemplateDoesNotExist`というエラーが表示される

+++

![TemplateDoesNotExist](elv_Jan_django_errorfriends/assets/part2/1_TemplateDoesNotExist.png)

---

### TemplateDoesNotExistの原因

> TemplateDoesNotExist: blog/post_list.html

- テンプレート`blog/post_list.html`をまだ作っていない
- まずテンプレートの空ファイルを用意する
- 次に記事一覧を表示できるように修正する

+++

### (3)テンプレートの空ファイルを用意する

作るファイル：`blog/templates/blog/post_list.html`

1. blogディレクトリにtemplatesディレクトリを作る
2. blog/templatesディレクトリにblogディレクトリを作る
3. blog/templates/blogディレクトリに空のpost_list.htmlを作る

+++

### （参考）テンプレートの名前空間

- なぜblog/templates/blogディレクトリに作成？
- templatesの下のアプリケーション名(blog)のディレクトリに作成することで、Djangoがテンプレートを区別できる（複数のアプリケーションが別々のpost_list.htmlを持つケース）
- ref: [はじめての Django アプリ作成、その 3](https://docs.djangoproject.com/ja/2.1/intro/tutorial03/)

+++

### テンプレートの空ファイルを用意する

- TemplateDoesNotExistは表示されなくなった
		- http://127.0.0.1:8000/
- 作りたいのは、ブログ記事の一覧画面
- ビューからテンプレートに渡されたpostsをテンプレートに表示したい

+++

### `post_list.html`表示内容

- 記事一覧には各記事の次のデータを表示
	- 公開日
	- タイトル
	- 本文

+++

### post_list.html

```html
<html>
    <head>
        <title>Django Girls blog</title>
    </head>
    <body>
        <div>
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>

        {% for post in posts %}
            <div>
                <p>published: {{ post.published_date }}</p>
                <h1><a href="">{{ post.title }}</a></h1>
                <p>{{ post.text|linebreaksbr }}</p>
            </div>
        {% endfor %}
    </body>
</html>
```

+++

### （参考）post_list.html 1/2

テンプレートタグ `{% for post in posts %}`

- ビューから渡されたpostsの1つ1つをpostとして取り出して処理
- Pythonのfor文のイメージ

+++

### （参考）post_list.html 2/2

- `{{ post.published_date }}`は記事の公開日の日付に置き換わる
- `{{ post.title }}`は記事のタイトルの文字列に置き換わる
- `{{ post.text|linebreaksbr }}`は記事の本文に置き換わる
	- `linebreaksbr`によって、本文の中の改行がHTMLでも表現される

+++

### 動作確認：ブログ記事を画面に表示する

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス
- **注**：テンプレートが見つからなくてTemplateDoesNotExistが表示されたままのときがある。その際はCtrl+Cで止めて、再度runserverする

+++

![ブログ記事が表示されています](elv_Jan_django_errorfriends/assets/part2/2_post_list.png)

---

### (4)CSS導入

- 一覧画面の見た目を整える
- 次のスライドの内容で`blog/static/css/blog.css`を作成
	- blogディレクトリの中にstaticディレクトリを作る
	- blog/staticディレクトリの中にcssディレクトリを作る
	- blog/static/cssディレクトリの中にblog.cssを作る

+++

### blog.css

```css
.page-header {
    background-color: #ff9400;
    margin-top: 0;
    padding: 20px 20px 20px 40px;
}

.page-header h1, .page-header h1 a, .page-header h1 a:visited, .page-header h1 a:active {
    color: #ffffff;
    font-size: 36pt;
    text-decoration: none;
}

.content {
    margin-left: 40px;
}

h1, h2, h3, h4 {
    font-family: 'Lobster', cursive;
}

.date {
    color: #828282;
}

.save {
    float: right;
}

.post-form textarea, .post-form input {
    width: 100%;
}

.top-menu, .top-menu:hover, .top-menu:visited {
    color: #ffffff;
    float: right;
    font-size: 26pt;
    margin-right: 20px;
}

.post {
    margin-bottom: 70px;
}

.post h1 a, .post h1 a:visited {
    color: #000000;
}
```

+++

### post_list.html アップデート

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
                	{% for post in posts %}
                        <div class="post">
                            <div class="date">
                                <p>published: {{ post.published_date }}</p>
                            </div>
                            <h1><a href="">{{ post.title }}</a></h1>
                            <p>{{ post.text|linebreaksbr }}</p>
                        </div>
                    {% endfor %}
                </div>
            </div>
        </div>
    </body>
</html>
```

+++

### （参考）post_list.html アップデート

- 1行目の`{% load static %}`：CSSを追加したことをテンプレートに教える
- Bootstrap3のクラスやblog.cssでスタイル定義したクラスを設定

+++

### CSS反映の確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス
- **注**：CSSが見つからなくてスタイルが反映されないことがある。その際はCtrl+Cで止めて、再度runserverする

+++

![CSS設定済みブログ一覧](elv_Jan_django_errorfriends/assets/part2/3_post_list_with_style.png)

+++

### ここまでの設定内容

- blog/urls.py：「`http://127.0.0.1:8000/`にアクセスされたら、blog/views.pyの`post_list`関数を使って対応する」と設定
- `post_list`関数：
	- 記事の一覧をPostモデルから取得
	- post_list.htmlテンプレートに記事のデータを埋め込んで表示する

+++

### ブログ記事を画面に表示する まとめ

- URLの設定（AttributeError）
- ビューの設定（TemplateDoesNotExist）
- テンプレートに表示
- CSS導入
