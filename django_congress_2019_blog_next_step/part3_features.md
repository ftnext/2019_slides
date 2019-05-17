### Agenda

- Django Girls Tutorial クイックツアー（10min）
- ユーザまわりを実装（10min）
- **この機能、どう作る？**（10min）
- まとめ（5min）
- 質疑（5min）

+++

### 誰でもコンテンツを作れるアプリ

- プログアプリのノウハウ + ユーザ管理
- 世の中のWebアプリで見かける「あの機能」はまだ実装されていない

+++

### この機能、どう作る？

1. ページネーション
2. 検索機能
3. ユーザの権限

---

### この機能、どう作る？

1. **ページネーション**
2. 検索機能
3. ユーザの権限

+++

### ページネーション

- 現状のブログアプリは一覧画面に全記事表示
- 1画面あたりに表示される記事が10件のように決まっているのをよく見かける
- 「ページング」とも言うそうです
- thinkAmiさんBlog [Djangoで、Paginatorやdjango-pure-paginationを使ってページングしてみた](https://thinkami.hatenablog.com/entry/2016/02/04/231901)を参考に、Bootstrapを当てて実装しています

+++

### ページネーションの例

![](django_congress_2019_blog_next_step/assets/part3/1_pagination.png)

+++

### ページネーションを実装する

- 一覧表示のジェネリックビュー（ListView）を使う
- テンプレートで、[Pageオブジェクト](https://docs.djangoproject.com/ja/2.2/topics/pagination/#page-objects)`page_obj`を使って、前後のページへのリンクを作る
- → post_listビューをジェネリックビューを使って書き換える

+++

### ビューの実装

```python
from django.views.generic import ListView

class PostList(ListView):
    # get_querysetで取得したデータを、context_object_nameという名前で
    # template_nameのテンプレートに渡すという設定をしている
    context_object_name = 'posts'
    template_name = 'blog/post_list.html'
    paginate_by = 2  # 1ページあたりの記事の数

    def get_queryset(self):
        posts = Post.objects.filter(published_date__lte=timezone.now())
        return posts
```

+++

### テンプレートの実装

```html
{% if is_paginated %}
  <nav aria-label="Page navigation">
    <ul class="pagination">
      <!-- 1つ前のページ -->
      {% if page_obj.has_previous %}
        <li class="page-item">
          <a class="page-link"
              href="{% url 'blog:post_list' %}?page={{ page_obj.previous_page_number }}"
              aria-label="Previous">
            ({{ page_obj.previous_page_number }})
            <span aria-hidden="true">&laquo;</span>
            <span class="sr-only">Previous</span>
          </a>
        </li>
      {% endif %}
      <!-- 現在のページ -->
      <li class="page-item active">
        <a class="page-link"
            href="{% url 'blog:post_list' %}?page={{ page_obj.number }}">
          {{ page_obj.number }}
        </a>
      </li>
      <!-- 1つ後のページ -->
      {% if page_obj.has_next %}
        <li class="page-item">
          <a class="page-link"
              href="{% url 'blog:post_list' %}?page={{ page_obj.next_page_number }}"
              aria-label="Next">
            <span aria-hidden="true">&raquo;</span>
            <span class="sr-only">Next</span>
             ({{ page_obj.next_page_number }})
          </a>
        </li>
      {% endif %}
    </ul>
  </nav>
{% endif %}
```

---

### この機能、どう作る？

1. ページネーション
2. **検索機能**
3. ユーザの権限

+++

### 検索

- Webアプリ内のコンテンツを検索できる機能をよく見かける（Twitter, Connpass）
- ブログアプリの記事を検索できるようにする（サイドバーblockに実装）

+++

### 検索のイメージ

![タイトルまたは本文に指定の語句を含む記事を検索しています](django_congress_2019_blog_next_step/assets/part3/2_search_keyword.png)

+++

### 検索を実装する

- サイドバーにフォームを用意（入力語句を記事一覧にGETで送信）
  - URL例：`http://127.0.0.1:8000/?keyword=すごい記事`
- PostListビューは、URLのkeywordの値を含む記事を絞って表示する

+++

### ビューの実装(`blog/views.py`)

```python
from django.views.generic import ListView

class PostList(ListView):
    context_object_name = 'posts'
    template_name = 'blog/post_list.html'
    paginate_by = 2

    def get_queryset(self):
        posts = Post.objects.filter(published_date__lte=timezone.now())
        keyword = self.request.GET.get('keyword')
        if keyword:
            # keywordが指定されているとき、タイトルにkeywordを含む記事を検索
            posts = posts.filter(title__icontains=keyword)
        return posts
```

+++

### 複数のフィールドを「または」で検索したければ

例：タイトルにkeywordを含む、または、本文にkeywordを含む

```python
# 該当部分のみ示しています
from django.db.models import Q

class PostList(ListView):
    def get_queryset(self):
        posts = Post.objects.filter(published_date__lte=timezone.now())
        keyword = self.request.GET.get('keyword')
        if keyword:
            posts = posts.filter(
                Q(title__icontains=keyword) | Q(text__icontains=keyword)
            )
        return posts
```

ref: naritoさんBlog [Djangoで、OR検索](https://narito.ninja/blog/detail/91/)

+++

### 検索欄にkeywordを残したい

- URLのkeywordに指定された値を検索欄（input要素）のvalueに持たせればよい
- URLのkeywordに指定された値を取得する **フィルタ** を実装する（カスタムフィルタ）
- フィルタ：テンプレートで`{{}}`の中に`|`を使って書くもの（例：`post.text|linebreaksbr`）
- ref: thinkAmiさんBlog [DjangoのListViewで、ページをフィルタしてみた](https://thinkami.hatenablog.com/entry/2016/03/17/003140)

+++

### フィルタを実装する

blog/templatetags/blog_customs.py

```python
from django import template
register = template.Library()

@register.filter(is_safe=True)
def parse_keyword(querydict):
    """GETのクエリパラメタを渡してkeyword(検索語句)を取り出す"""
    keyword = querydict.get('keyword')
    return keyword if keyword else ''
```

+++

### テンプレートでカスタムフィルタを使う

`blog/post_list.html`

```html
{% load blog_customs %}

<!-- 実際のHTMLを簡略化して表示しています -->
<form method="GET" action="{% url 'blog:post_list' %}">
  <input type="text" name="keyword" value="{{ request.GET|parse_keyword }}">
  <button type="submit">Search</button>
</form>
```

+++

### 参考：検索結果をページネーションさせたい

時間があったときに扱うコンテンツです

- 検索結果を表示した際に次のページのリンクをクリックすると、検索の絞り込みが解除されてしまう
- 原因はURLでkeywordパラメタが消えてしまうため（`http://127.0.0.1:8000/?page=2`）

+++

### 検索結果のページネーション

- 検索結果の◯ページ目のURL例
  - `http://127.0.0.1:8000/?keyword=すごい記事&page=2`
- `page=2`というパラメタを追加するタグを作る（カスタムタグ）
- タグ：テンプレートで`{% %}`として書くもの（例：`{% url 'blog:post_list' %}`）

+++

### タグを実装する

blog/templatetags/blog_customs.py

```python
from django import template
register = template.Library()

@register.simple_tag
def query_replace(request, field, value):
    """GETのクエリ文字列にパラメタfieldと値valueを追加する"""
    url_dict = request.GET.copy()
    url_dict[field] = value
    return url_dict.urlencode()
```

+++

### テンプレートでカスタムタグを使う

- ページネーションのURL作成部分を変更（一例のみ示す）
- `http://127.0.0.1:8000/?keyword=すごい記事` のとき、hrefは`http://127.0.0.1:8000/?keyword=すごい記事&page=2`となります

```html
<!-- 1つ前のページ -->
{% if page_obj.has_previous %}
  <li class="page-item">
    <!-- hrefの?の右側が変わっています -->
    <!-- 変更前 ?page={{ page_obj.previous_page_number }} -->
    <a class="page-link"
        href="{% url 'blog:post_list' %}?{% query_replace request 'page' page_obj.previous_page_number %}"
        aria-label="Previous">
      ({{ page_obj.previous_page_number }})
      <span aria-hidden="true">&laquo;</span>
      <span class="sr-only">Previous</span>
    </a>
  </li>
{% endif %}
```

---

### この機能、どう作る？

1. ページネーション
2. 検索機能
3. **ユーザの権限**

+++

### ブログアプリの要件

- ユーザ登録を実装したが、誰にでも記事を書かせたくはない
- → ユーザに権限をつけてコントロールする

+++

TODO：あとで書く
