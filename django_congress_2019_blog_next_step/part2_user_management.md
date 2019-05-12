### Agenda

- Django Girls Tutorial クイックツアー（10min）
- **ユーザまわりを実装**（10min）
- この機能、どう作る？（10min）
- まとめ（5min）
- 質疑（5min）

+++

### ブログアプリをもとにすると

- **特定のユーザがコンテンツを更新するサイト** が作れる
- 例：管理ユーザだけがコンテンツを更新するポータルサイト
- あまりメジャーではない

+++

### 世の中のWebアプリは

- ユーザは誰でもコンテンツを作れる
- 例：Twitter, Connpass, MF請求書

+++

### 誰でもコンテンツを作れるアプリを目指して

- プログアプリのノウハウ + **ユーザ管理**（ユーザ登録、パスワード再設定など）
- そこで、Django Girls Tutorialにない **ユーザの扱い** について取り上げます

+++

### ユーザ管理までの道のり

1. クラスベースビュー
2. ジェネリックビュー
3. ユーザ管理
4. +α：権限

---

### ユーザ管理までの道のり

1. **クラスベースビュー**
2. ジェネリックビュー
3. ユーザ管理
4. +α：権限

+++

### Djangoのビューの書き方は2通り

- Django Girls Tutorialで書いてきたビューは **関数ベース** ビュー
- クラスを使って書く **クラスベース** ビューを紹介
- post_newビューを2通りで書いてみます（次のスライド）

+++

@snap[west span-100]
```python
from django.contrib.auth.decorators import login_required
from django.shortcuts import redirect, render
from .forms import PostForm

@login_required
def post_new(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.save()
            return redirect('blog:post_detail', pk=post.pk)
    else:
        form = PostForm()
    return render(request, 'blog/post_edit.html', {'form': form})
```
@snapend

@snap[east span-100]
```python
from django.contrib.auth.mixins import LoginRequiredMixin
from django.shortcuts import redirect, render
from django.views import View
from .forms import PostForm

class PostNewView(LoginRequiredMixin, View):
    form_class = PostForm
    template_name = 'blog/post_edit.html'

    def get(self, request, *args, **kwargs):
        form = self.form_class()
        return render(request, self.template_name, {'form': form})

    def post(self, request, *args, **kwargs):
        form = self.form_class(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.save()
            return redirect('blog:post_detail', pk=post.pk)
        return render(request, self.template_name, {'form': form})
```
@snapend

+++

### 2つの違い

関数ベースビュー | クラスベースビュー
----- | -----
`request.method == 'POST'`という条件分岐 | `get`, `post`というHTTPメソッドに対応するメソッドを定義。<br>クラスのプロパティを使用（`self.form_class`）

書き換えられると紹介しましたが、  
クラスベースビューは関数ベースのビューを完全に置き換えるものではないそうです（[クラスベースビュー入門](https://docs.djangoproject.com/ja/2.2/topics/class-based-views/intro/)）

---

### ユーザ管理までの道のり

1. クラスベースビュー
2. **ジェネリックビュー**
3. ユーザ管理
4. +α：権限

+++

### ジェネリックビュー

- どんなWebアプリでも使う共通処理がある
  - 例：データベースのデータの **一覧、詳細**
- 共通処理を扱うための抽象的なクラスベースビューがDjangoに用意されている＝ジェネリックビュー

+++

@snap[north span-100]
### 例1：post_listビューをジェネリックビューで書き換える
@snapend

@snap[west span-100]
```python
from django.shortcuts import render
from .models import Post

def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now())
    return render(request, 'blog/post_list.html', {'posts': posts})
```
@snapend

@snap[east span-100]
```python
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    # querysetで取得したデータを
    # context_object_nameという名前でテンプレートに渡すという設定をしている
    context_object_name = 'posts'
    queryset = Post.objects.filter(published_date__lte=timezone.now())
```
@snapend

+++

### 例2：ExtensionsのLoginViewはジェネリックビュー

TODO：デフォルトの設定で使っていることを書く

+++

### ジェネリックビューにも限界はある

>ジェネリックビューは実質的に開発をスピードアップさせてくれます。しかし、多くのプロジェクトでは遅かれ早かれジェネリックビューだけでは十分ではなくなる瞬間が訪れます。

ref: [ビルトインのクラスベースのジェネリックビュー](https://docs.djangoproject.com/ja/2.2/topics/class-based-views/generic-display/)

+++

### 私見：ジェネリックビューとの付き合い方

- Webサイトでよくある機能を早く作れるので、個人開発では便利そう
- 実務では使わないという選択も考えられるので、依存しないように注意
- （実務経験がない立場からの意見ですので、フィードバック歓迎です）

---

### ユーザ管理までの道のり

1. クラスベースビュー
2. ジェネリックビュー
3. **ユーザ管理**
4. +α：権限

+++

### ユーザ管理の実装内容

- ユーザ管理用のジェネリックビューを設定して使う
- `django.contrib.auth.views`にユーザ登録、パスワード再設定など用意されている
- クラスベースビューを使う知識が必要

+++

### ユーザ管理の実装

- ユーザ登録
- パスワード再設定（パスワードを忘れた場合の対応）

TODO：続きを書く

---

### ユーザ管理までの道のり

1. クラスベースビュー
2. ジェネリックビュー
3. ユーザ管理
4. **+α：権限**

+++

### ブログアプリの要件

- ユーザ登録を実装したが、誰にでも記事を書かせたくはない
- → ユーザに権限をつけてコントロールする
