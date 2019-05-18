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

[ソースコード tag:3-more_features](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/3-more_features)

---

### この機能、どう作る？

1. **ページネーション**
2. 検索機能
3. ユーザの権限

[ソースコード tag:3-more_features](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/3-more_features)

+++

### ページネーション（ページングとも）

- 現状のブログアプリは一覧画面に全記事表示
- 1画面あたりに表示される記事が10件のように決まっているのをよく見かける（検索結果など）
- thinkAmiさんBlog [Djangoで、Paginatorやdjango-pure-paginationを使ってページングしてみた](https://thinkami.hatenablog.com/entry/2016/02/04/231901)を参考に、Bootstrapを当てて実装しています

+++

### ページネーションの例

<span class="sixty-percent-img">
![](django_congress_2019_blog_next_step/assets/part3/1_pagination.png)
</span>

+++

### ページネーションを実装する

- 一覧表示のジェネリックビュー（ListView）を使う方法を選択（実装簡単）
- テンプレートで、[Pageオブジェクト](https://docs.djangoproject.com/ja/2.2/topics/pagination/#page-objects)`page_obj`を使って、前後のページへのリンクを作る

+++

### ビューの実装

```python
from django.views.generic import ListView

class PostList(ListView):
    # get_querysetで取得したデータを、context_object_nameという名前で
    # template_nameのテンプレートに渡すという設定をしている
    context_object_name = 'posts'
    template_name = 'blog/post_list.html'
    paginate_by = 2  # 1ページあたりの記事の数（ページネーションの設定はここだけ）

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
          <!-- http://127.0.0.1:8000/?page=1 のようなURLになる -->
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

[ソースコード tag:3-more_features](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/3-more_features)

+++

### 検索

- Webアプリ内のコンテンツを検索できる機能をよく見かける（Twitter, Connpass）
- ブログアプリの記事を検索できるようにする（サイドバーblockに実装）

+++

### 検索のイメージ

<span class="sixty-percent-img">
![タイトルまたは本文に指定の語句を含む記事を検索しています](django_congress_2019_blog_next_step/assets/part3/2_search_keyword.png)
</span>

+++

### 検索を実装する

- サイドバーにフォームを用意（入力語句をkeywordパラメタの値に設定）
  - URL例：`http://127.0.0.1:8000/?keyword=すごい記事`
- PostListビューは、keywordパラメタの値を含む記事に絞って表示する

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

ref: naritoさんBlog [Djangoで、OR検索](https://narito.ninja/blog/detail/91/)

```python
# 該当部分のみ示しています
from django.db.models import Q

class PostList(ListView):
    def get_queryset(self):
        posts = Post.objects.filter(published_date__lte=timezone.now())
        keyword = self.request.GET.get('keyword')
        if keyword:
            posts = posts.filter(
                # タイトルにkeywordを含む、または、本文にkeywordを含む
                Q(title__icontains=keyword) | Q(text__icontains=keyword)
            )
        return posts
```

+++

### 検索欄にkeywordを残したい

- ここまででは検索結果の検索欄は空（検索語句はURLに残る）
- keywordパラメタの値を検索欄（input要素）のvalue属性に持たせればよい

+++

### クエリ文字列からパラメタの値を取得

- keywordパラメタの値を取得する **フィルタ** を実装する（カスタムフィルタ）
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

```html
<!-- 1つ前のページ -->
{% if page_obj.has_previous %}
  <li class="page-item">
    <!-- hrefの?の右側が変わっています -->
    <!-- 変更前 ?page={{ page_obj.previous_page_number }} -->
    <!-- http://127.0.0.1:8000/?keyword=すごい記事&page=2 のようになります -->
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

[ソースコード tag:3-more_features](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/3-more_features)

+++

### ブログアプリの要件

- ユーザ登録を実装したが、誰にでも記事を書かせたくはない
- 現状は、登録したユーザは記事を書ける
- → ユーザのできることをコントロールする

+++

### 権限（permission）

- ユーザができること（記事を作成できる、など）
- アプリの中のモデルごとに、権限が用意される（`INSTALLED_APPS`に`django.contrib.auth`が設定されている場合）

ref: [権限と認可](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#permissions-and-authorization)

+++

### 権限：`アプリ.できること_モデル`

- できることは4種類
  - view（見られる）
  - add（作成できる）
  - change（編集できる）
  - delete（削除できる）
- `'blog.add_post'`＝記事が書ける


+++

### グループ（Group）

- ユーザ一人ひとりに権限を付与するのは、権限が増えると　大変そう
- 権限をグループにまとめ、ユーザをグループに所属させる
- 記事の閲覧だけできる権限からなるグループを作成

+++

### 記事を閲覧だけできるグループを作成

Django AdminからGUIで操作

<span class="sixty-percent-img">
![](django_congress_2019_blog_next_step/assets/part3/3_create_Readeruser_Group.png)
</span>

+++

### ユーザ登録時に権限を付与

```python
from django.contrib.auth.models import Group

class Register(CreateView):
    # ユーザ登録フォームから作成されたユーザにはReaderUserグループを付与する
    # 変数の設定は変更なし
    def form_valid(self, form):
        user = form.save()
        group = Group.objects.get(name='ReaderUser')
        user.groups.add(group)
        return super().form_valid(form)
```

+++

### ビュー：権限設定

- 関数ベースビュー：`@permission_required`
- クラスベースビュー：`PermissionRequiredMixin`

+++

### 関数ベースビューの例

```python
from django.contrib.auth.decorators import permission_required

@login_required
@permission_required('blog.change_post', raise_exception=True)
def post_edit(request, pk):
    # 処理は変更なし

@login_required
@permission_required('blog.delete_post', raise_exception=True)
def post_remove(request, pk):
  　# 処理は変更なし
```

+++

### クラスベースビューの例

```python
from django.contrib.auth.mixins import PermissionRequiredMixin

class PostNew(LoginRequiredMixin, PermissionRequiredMixin, CreateView):
    permission_required = 'blog.add_post'  # 権限設定の変数

    # 他の変数やメソッドは変更なし
```

+++

### 権限がない場合

![読者ユーザで記事を編集しようとしても403エラー](django_congress_2019_blog_next_step/assets/part3/4_permission_denied.png)

+++

### テンプレート：権限がなければ表示しない

`perms.アプリ.できること_モデル`を確認して出し分ける

```html
{% if perms.blog.add_post %}
  <a href="{% url 'blog:post_new' %}" class="top-menu">
    <i class="fas fa-plus"></i>
  </a>
{% endif %}
```

+++

### カスタムな権限

時間があったときに扱うコンテンツです

- view, add, change, delete以外にも権限が必要（例：公開）
- モデルでカスタム権限を作成する（権限の種類を増やす）
- マイグレーションが必要

+++

### モデル：Metaクラスでpermissionsを定義

```python
class Post(models.Model):
    # Metaクラス以外には変更なし
    class Meta:
        ordering = ['-published_date', '-created_date']  # この行は変更なし
        permissions = [
            ('publish_post', 'Can publish a draft post'),
            ('view_draft_posts', 'Can view draft posts'),
        ]
```

+++

### カスタムパーミッションを設定する

- デフォルトの権限と使い方は同じ
- ビュー：`permission_required`または`PermissionRequiredMixin`
- テンプレート：permsを確認

+++

### 見せたくないところは読者に見せないようにできました

![記事の作成や、ドラフトの閲覧、公開された記事の編集ができません](django_congress_2019_blog_next_step/assets/part3/5_permission_for_reader.png)

---

### まとめ：ユーザまわりを実装

- ListViewを使ったページネーション
- 検索 + カスタムフィルタ／タグ
- グループでユーザに権限付与
  - ビューで権限設定、テンプレートで権限確認
