### 【エラーは友達】<br>Django基礎ハンズオン

1. 管理画面からブログ記事を作る（30分）
2. ブログ記事を画面に表示する（40分）
3. <div class="django-girls-highlight">ブログ画面からブログ記事を作る（40分）</div>

+++

### ブログ画面からブログ記事を作る

- 現状：記事は管理画面から作ることができる
- 管理画面以外からも記事を作れるようにしたい

+++

### ブログ画面からブログ記事を作る ゴール

- 記事一覧ページ`http://127.0.0.1:8000/`にリンクを追加
- リンクから記事の作成フォームに遷移する
- フォームから記事が作成できる
- ※管理画面にログインしているユーザ以外にはリンクを見せない

+++

### ブログ画面からブログ記事を作る

1. 記事作成フォーム設定
2. フォームに遷移できるようにする
3. フォームから保存できるようにする

---

### フォーム

- 入力欄の集まり
		- 例：connpassでイベント申し込み。参加コメントを入力
- フォームを通してデータを作成・更新

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
- `fields`：フォームには記事のタイトルと本文が入力できるようにする

---

### (2)フォームに遷移できるようにする

- 「Django Girls Blog」という見出し部分に、**記事作成フォームへのリンクを追加** する
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

### 動作確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### 第3のエラー NoReverseMatch

記事一覧ページではなく`NoReverseMatch`というエラーが表示される😱

![](elv_Jan_django_errorfriends/assets/part3/1_NoReverseMatch.png)

+++

### NoReverseMatchの原因

> Reverse for 'post_new' not found.

- 追加したaタグ `href="{% url 'post_new' %}"`
- `{% url %}`タグは、urls.pyの`urlpatterns`の中から`name='post_new'`と設定されているURLを返す
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

### NoReverseMatch解消確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`

+++

### AttributeError

- コマンドラインを見ると、サーバが起動していない

> AttributeError: module 'blog.views' has no attribute 'post_new'

+++

### AttributeErrorを思い出す

- 先ほどはurlpatternsで設定した`post_list`関数がblog/views.pyの中にないために発生
	- `path('', views.post_list, name='post_list')`

+++

### AttributeErrorの原因

- 直近でurlpatternsで設定した`post_new`関数もまだblog/views.pyの中に用意していない💡
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

### AttributeError解消確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリックする

+++

### TemplateDoesNotExist

記事作成アイコン（リンク）をクリックした後の画面

![](elv_Jan_django_errorfriends/assets/part3/2_TemplateDoesNotExist.png)

+++

### TemplateDoesNotExistを思い出す

- 先ほどは`blog/templates/blog/post_list.html`を作っていなかったために発生
	- `render(request, 'blog/post_list.html', {'posts': posts})`

+++

### TemplateDoesNotExistの原因

- 今回も`blog/templates/blog/post_edit.html`を作っていない💡
	- `render(request, 'blog/post_edit.html', {'form': form})`

+++

### テンプレート blog/post_edit.html 作成

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

### （参考）テンプレート blog/post_edit.html (1/2)

- `{{ form.as_p }}`：フォームに必要な入力欄を表示
- `{% csrf_token %}`：セキュリティ対策（クロスサイトリクエストフォージェリ）
	- このタグをつけ忘れるとエラーが出る（タグをつけることで解決）

+++

### （参考）テンプレート blog/post_edit.html (2/2)

`<form>`タグ

- action属性が指定されていない
- **フォームが表示されているページ自身に対して** 入力されたデータを送信する設定

+++

### 動作確認：フォームに遷移できるようにする

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリックする

+++

![フォームに遷移できました](elv_Jan_django_errorfriends/assets/part3/3_display_form.png)

---

### (3)フォームから保存できるようにする

1. 記事作成フォームから記事を保存できるようにする（`post_new`関数の修正）
2. 記事作成フォームへのリンクを管理画面でログインしているユーザだけに見せる

+++

### (3-1)blog/views.py アップデート

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

### （参考）`post_new`関数の修正 1/4

`request.method == "POST"`

条件 | 条件式の値 | 後続処理
----- | ----- | -----
記事作成ページに遷移 | False | フォーム表示
記事作成ページに入力されたデータを送信 | True | 入力内容の検証／保存

+++

### （参考）`post_new`関数の修正 2/4

- `form = PostForm(request.POST)`：入力された内容でPostFormを作成
- `form.is_valid()`：入力値の検証
	- 入力値に不備がない場合、Trueとなる（保存処理に進む）
	- 入力値に不備がある場合、Falseとなる（入力値を保ったフォームを再表示する）

+++

### （参考）`post_new`関数の修正 3/4

記事の保存処理

- `post = form.save(commit=False)`：入力値を元に記事を作成（まだ保存しない）
- 記事に作成者と公開日が未設定のため設定する
- 未設定の項目がなくなったため、`post.save()`で保存する

+++

### （参考）`post_new`関数の修正 4/4

- `return redirect('post_list')`：記事一覧画面を表示する
- 記事を保存したら、記事一覧画面に遷移する
- （記事を保存できなかったら、記事作成画面のまま）

+++

### 動作確認：フォームから保存できるようにする

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリック→記事を作成してみる

+++

![フォームから記事を作成](elv_Jan_django_errorfriends/assets/part3/4_post_from_form.png)

+++

### 作成されました

<span class="sixty-percent-img">
![一覧ページに遷移](elv_Jan_django_errorfriends/assets/part3/5_post_created_from_form.png)
</span>

+++

### (3-2)記事作成フォームへのリンクの表示を修正

- 管理画面でログインしているユーザだけに見せる
- **注**：これはセキュリティ対策としては不十分です（ログインしているユーザだけが記事を**作成**できるようにするべき）

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

### `{% if user.is_authenticated %}`

- Pythonのif文のイメージ
- アクセスしたユーザが管理画面でログインしている場合、True
- 管理画面でログインしていないユーザについてはFalse

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

### 書き換えた2つのテンプレート

- post_list.htmlとpost_edit.htmlには共通部分が多い
- 共通部分を「基本テンプレート」に切り出せる
- 詳しくはAppendix参照

+++

### ブログ画面からブログ記事を作る

- 記事作成フォーム設定（forms.py）
- フォームに遷移できるようにする
		- NoReverseMatch、AttributeError、TemplateDoesNotExist
- フォームから保存できるようにする
