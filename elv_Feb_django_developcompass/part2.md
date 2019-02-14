### 【羅針盤を手に入れる】<br>Django基礎ハンズオンⅡ

0. ブログアプリの機能のおさらい（10分）
1. ブログ画面からブログ記事を作る（40分）
2. <div class="django-girls-highlight">ブログ記事の詳細が見られるようにする（30分）</div>
3. ブログ記事に画像を追加できるようにする（30分）

+++

### ブログ記事の詳細

- 現状：一覧には記事の公開日時、タイトル、本文を表示している
- 記事の作成者や作成日時も見たい
- 1個1個の記事についてそれぞれのページを用意したい（記事の詳細画面）

+++

### ブログ記事の詳細が見られるようにする ゴール

- 記事一覧の記事のタイトルを詳細画面へのリンクにする
- 記事の詳細のURLの例：`http://127.0.0.1:8000/post/1/`
- 記事の詳細では、公開日時、タイトル、本文の他、作成者や作成日時も見られる

+++

### ゴール - 現状

- blog/post_list.htmlに記事詳細へのリンク追加
- 記事詳細画面用のURL、ビュー、テンプレートが必要
- 疑問：例えばブログ記事が3つあるとき、URL、ビュー、テンプレートはそれぞれいくつ必要？

+++

### 羅針盤のうち何が必要？

<span class="eighty-percent-img">
![テンプレート？URL設定？モデル？ビュー？](elv_Feb_django_developcompass/assets/django_compass.png)
</span>

+++

### 羅針盤に照らして 1/2

新しくページを作る（詳細ページ）

- リンク
- URL設定
- ビュー
- テンプレート

+++

### 羅針盤に照らして 2/2

- モデルは変更しない
- 新しいデータ項目を設けるわけではない

+++

### 羅針盤

<span class="eighty-percent-img">
![1.既存テンプレート、2.URL、3.ビュー、4.新規テンプレート](elv_Feb_django_developcompass/assets/part2/django_compass_part2.001.png)
</span>

+++

### ブログ記事の詳細が見られるようにする

1. リンク追加
2. URL設定
3. ビュー作成
4. テンプレート作成

---

### (1)リンクを追加する

<span class="eighty-percent-img">
![](elv_Feb_django_developcompass/assets/part2/django_compass_part2.002.png)
</span>

+++

### リンクの追加にあたって

- 方針：記事の持つID(1,2,3,...)を利用する
- 例えば、ID=1の記事を表示するパスは、`post/1/`
- IDを使えば、記事が増えていってもリンクを自動で決めることができる

+++

### リンク追加（post_list.html）

```html
    {% for post in posts %}
        <div class="post">
            <div class="date">
                <p>published: {{ post.published_date }}</p>
            </div>
            <!-- 以下のaタグのhref属性のみ変更 -->
            <h1><a href="{% url 'post_detail' pk=post.pk %}">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaksbr }}</p>
        </div>
    {% endfor %}
```

+++

### 動作確認（一覧画面にリンク追加）

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### NoReverseMatch

![](elv_Feb_django_developcompass/assets/part2/1_NoReverseMatch.png)

「原因は〇〇で、☆☆すると解決」

+++

### NoReverseMatchの原因と解決策

>Reverse for 'post_detail' not found.

- blog/urls.pyに`name='post_detail'`というURLを設定する
- 手順2で実施します

+++

### （参考）{% url 'post_detail' pk=post.pk %}

- `{% url %}`タグについて
- pk=post.pkについて

+++

### （参考）`{% url %}`

- urls.pyの`urlpatterns`の中から`name`が一致するURLのパスを返す
- ビューがテンプレートにデータを埋め込む中で、`{% url %}`はパスに置き換わる（今回は置き換えに失敗してエラー）

+++

### （参考）`{% url %}` 使用例（base.html）

```html
{% if user.is_authenticated %}
    <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
{% endif %}
```

- blog/urls.pyの設定：`path('post/new/', views.post_new, name='post_new')`
- `{% url %}`は`/post/new/`というパスに置き換わる

+++

### （参考）`pk=post.pk`

- post.pkは記事のID（具体例：1, 108）
- 記事の詳細のURLを作る際に記事のIDが必要（`{% url %}`タグの中に指定する）
- 例）ID=1の記事の詳細画面：`{% url 'post_detail' pk=1 %}`→ URLは`post/1/`

+++

### （参考）pkはprimary keyの略

- pk：主キー
- migrateでIDをpkとして設定した(IDは整数値)
- 参考：[はじめての Django アプリ作成、その2](https://docs.djangoproject.com/ja/2.1/intro/tutorial02/#activating-models)
- 実は、pkはID(整数値)でなくてもよい（一意であり空の値をとらなければ主キーとして使える）

---

### (2)URLを設定する

<span class="eighty-percent-img">
![](elv_Feb_django_developcompass/assets/part2/django_compass_part2.003.png)
</span>

+++

### NoReverseMatchの解決（blog/urls.py）

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('post/new/', views.post_new, name='post_new'),
    # 以下の1行を追加
    path('post/<int:pk>/', views.post_detail, name='post_detail'),
]
```

+++

### `'post/<int:pk>/'`

- パスのパターンを表す（パターンで指定することで1つ1つ指定しなくてよい）
- 例：post/1/やpost/108/が該当
- `<int:pk>`の部分の整数がpkという変数に入る(post/108/の場合はpk=108となる)

+++

### NoReverseMatch解消確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`

+++

### AttributeError

> AttributeError: module 'blog.views' has no attribute 'post_detail'

「原因は〇〇で、☆☆すると解決」（機能を用意しなくていいので手を動かしてみてください）

+++

### AttributeErrorの原因と解決策

- 原因は、blog/urls.pyの`path('post/<int:pk>/', views.post_detail, name='post_detail')`
- blog/@color[#ff9400](views.py)に@color[#ff9400](`post_detail`関数を用意する)

+++

### blog/views.pyに`post_detail`関数追加

パスに指定された記事のIDを受け取るために、pkという引数を持たせる

```python
# importに変更なし
from django.shortcuts import redirect
from django.shortcuts import render
from django.utils import timezone
from .forms import PostForm
from .models import Post

# post_list, post_newにも変更なし

# 以下を追加（引数のpkがポイント）
def post_detail(request, pk):
    # 手順3で一緒に追加します
```

---

### (3)記事を表示するためのビューを作る

<span class="eighty-percent-img">
![](elv_Feb_django_developcompass/assets/part2/django_compass_part2.004.png)
</span>

+++

### `post_detail`関数の行う処理

1. パスに指定されたpkの記事を取得
2. 記事をテンプレートに渡す
3. テンプレートに記事のデータを埋め込んで表示する

+++

### blog/views.py

```python
from django.shortcuts import get_object_or_404 # 追加
from django.shortcuts import redirect
from django.shortcuts import render
from django.utils import timezone
from .forms import PostForm
from .models import Post

# post_list, post_newは変更しない

def post_detail(request, pk):
    post = get_object_or_404(Post, pk=pk) # 1にあたる
    return render(request, 'blog/post_detail.html', {'post': post}) # 2と3にあたる
```

+++

### `post_detail`関数

- `post = get_object_or_404(Post, pk=pk)`
    - URLで指定されたpkの記事を取得
- `render(request, 'blog/post_detail.html', {'post': post})`
    - 記事をテンプレートに渡す：`{'post': post}`
    - テンプレートに記事のデータを埋め込んで表示する：`render`

+++

### （参考）`get_object_or_404`

- 存在しない記事のURLにはエラーページを出す（カスタマイズ可能）
- 記事を単に`get`すると、存在しない記事のURLの際はDoesNotExistというエラーになる
- `get_object_or_404`を使えば、DoesNotExistというエラーは出ない

+++

### 手順1でリンクに追加したURLについて

- ID=1の記事のタイトルには`post/1/`というパスでリンクが設定される（`{% url 'post_detail' pk=post.pk %}`）
- ID=1の記事のタイトルをクリックすると、`post/<int:pk>/`というURL設定に該当し、`post_detail`関数のpk引数に1が渡る

+++

### 動作確認 1/2

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### 動作確認 2/2

![記事のタイトル部分をクリック](elv_Feb_django_developcompass/assets/part2/2_click_post_title.png)

+++

### TemplateDoesNotExist

![](elv_Feb_django_developcompass/assets/part2/3_TemplateDoesNotExist.png)

「原因は〇〇で、☆☆すると解決」（機能を用意しなくていいので手を動かしてみてください）

+++

### TemplateDoesNotExistの原因と解決策

> TemplateDoesNotExist: blog/post_detail.html

- blog/templates/blog/post_detail.htmlを作成する
- 空のファイルを用意し、中身は手順4で追加します

---

### (4)テンプレートに記事の詳細を表示する

<span class="eighty-percent-img">
![](elv_Feb_django_developcompass/assets/part2/django_compass_part2.005.png)
</span>

+++

### 詳細画面の表示項目（振り返り）

- 公開日時(published_date)
- タイトル(title)
- 本文(text)
- 作成者(author)
- 作成日時(created_date)

+++

### blog/post_detail.html

```html
{% extends 'blog/base.html' %}

{% block content %}
    <div class="post">
        <div class="date">
            {% if post.published_date %}
                <p>published: {{ post.published_date }}</p>
            {% endif %}
            <p>created: {{ post.created_date }}</p>
        </div>
        <h1>{{ post.title }}</h1>
        <p><em>Author: {{ post.author }}</em></p>
        <p>{{ post.text|linebreaksbr }}</p>
    </div>
{% endblock %}
```

+++

### 動作確認

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス
- 記事のタイトル部分をクリック

+++

![記事の詳細が見られました！](elv_Feb_django_developcompass/assets/part2/4_display_detail.png)

+++

### テンプレートは1つだけでよい

- 詳細画面のパスのパターンではpkが指定される（`'post/<int:pk>/'`）
- ビューはモデルからpkに応じた記事を取得し、テンプレートに渡す
- テンプレートは記事について表示することだけを考える（Postの項目が表示できればいい）

+++

### 公開されていない記事も詳細が見られます

<span class="sixty-percent-img">
![](elv_Feb_django_developcompass/assets/part2/5_not_published_post.png)
</span>

URL例：http://127.0.0.1:8000/post/3

+++

### まとめ：ブログ記事の詳細が見られるようにする

1. リンク追加 `{% url %}`
2. URL設定 `'post/<int:pk>/'`
3. ビュー作成 `post_detail`関数
4. テンプレート作成 blog/post_detail.html
