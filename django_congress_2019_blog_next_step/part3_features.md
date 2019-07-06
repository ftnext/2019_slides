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
2. @css[omitted-item](検索機能)
3. ユーザの権限

[ソースコード tag:3-more_features](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/3-more_features)

---

### この機能、どう作る？

1. **ページネーション**
2. @css[omitted-item](検索機能)
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
2. @css[omitted-item](検索機能)
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

### まとめ：この機能、どう作る？

- ListViewを使ったページネーション
- グループでユーザに権限付与
  - ビューで権限設定、テンプレートで権限確認

+++?color=#ccffcc

### 参考：さらに進んだ権限

「[Authorization in Django](https://gitpitch.com/hirokiky/gitpitch?p=2019djangocongress)」  
DjangoCongress 2019 kyさん  
[YouTube](https://www.youtube.com/watch?v=gaS2vi4wOMQ)

+++?color=#ccffcc

### 初演から省略したトピック

- [検索機能（検索 + カスタムフィルタ／タグ）](https://gitpitch.com/ftnext/2019_slides/master?p=django_congress_2019_blog_next_step#/16)

興味がある方は初演スライドをご確認ください
