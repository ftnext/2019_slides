### Agenda

- Django Girls Tutorial クイックツアー（10min）
- **ユーザまわりを実装**（10min）
- この機能、どう作る？（10min）
- まとめ（5min）
- 質疑（5min）

+++

### ブログアプリをもとにすると

- **特定のユーザがコンテンツを更新するサイト** が作れる
- 例1：管理ユーザだけがコンテンツを更新するポータルサイト
- 例2：自分だけで使うタスク管理アプリ

+++

### 世の中のWebアプリは

- ユーザは誰でもコンテンツを作れる
- 例：Twitter（ツイート）, Connpass（イベント）

+++

### 誰でもコンテンツを作れるアプリを目指して

- プログアプリのノウハウ + **ユーザ管理**（ユーザ登録、パスワード再設定など）
- そこで、Django Girls Tutorialにない **ユーザの扱い** について取り上げます

+++

### ユーザ管理までの道のり

1. クラスベースビュー
2. ユーザ作成（ジェネリックビュー）
3. ユーザ管理（認証ビュー）

---

### ユーザ管理までの道のり

1. **クラスベースビュー**
2. ユーザ作成（ジェネリックビュー）
3. ユーザ管理（認証ビュー）

+++

### Djangoのビューの書き方は2通り

- Django Girls Tutorialで書いてきたビューは **関数ベース** ビュー
- クラスを使って書く **クラスベース** ビューを紹介
- post_newビューを2通りで書いてみます（次のスライド）

+++

@snap[west span-50 text-center]

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

@snap[east span-50 text-center]

```python
from django.contrib.auth.mixins import LoginRequiredMixin
from django.shortcuts import redirect, render
from django.views import View
from .forms import PostForm

class PostNew(LoginRequiredMixin, View):
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
`request.method == 'POST'`という条件分岐 | `get`, `post`というHTTPメソッドに対応するメソッドを定義。<br>クラスのプロパティを使用（`self.form_class`）<br>`path('post/new/', views.PostNew.as_view(), name='post_new'),`

書き換えられると紹介しましたが、  
クラスベースビューは関数ベースのビューを完全に置き換えるものではないそうです（[クラスベースビュー入門](https://docs.djangoproject.com/ja/2.2/topics/class-based-views/intro/)）

---

### ユーザ管理までの道のり

1. クラスベースビュー
2. **ユーザ作成（ジェネリックビュー）**
3. ユーザ管理（認証ビュー）

+++

### ジェネリックビュー

- どんなWebアプリでも使う共通処理がある
  - 例：データベースのデータの **一覧、詳細** など
- 共通処理を扱うための抽象的なクラスベースビューがDjangoに用意されている（`django.views.generic`）

+++

### ジェネリックビュー 一覧

- display（一覧、詳細）
- edit（作成、更新、削除）
- date（アーカイブ。単位：年・月・週など）

[ビルトインのクラスベースビュー API](https://docs.djangoproject.com/ja/2.2/ref/class-based-views/)

+++

@snap[north span-100]
### 作成のジェネリックビューの例：CreateView
@snapend

@snap[west center]
```python
# クラスベースビューで書いたpost_newビュー
from django.contrib.auth.mixins import LoginRequiredMixin
from django.shortcuts import redirect, render
from django.views import View
from .forms import PostForm

class PostNew(LoginRequiredMixin, View):
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

@snap[east center]
```python
# CreateViewを使って書き換え
from django.contrib.auth.mixins import LoginRequiredMixin
from django.shortcuts import redirect
from django.views.generic import CreateView
from .forms import PostForm
class PostNew(LoginRequiredMixin, CreateView):
    form_class = PostForm
    template_name = 'blog/post_edit.html'

    # カスタマイズしたい処理だけ上書きする
    # 入力値に問題がないときに呼ばれる処理。authorを設定するように上書きする
    def form_valid(self, form):
        post = form.save(commit=False)
        post.author = self.request.user
        post.save()
        return redirect('blog:post_detail', pk=post.pk)
```
@snapend

+++

### ジェネリックビューを使う

- ジェネリックビューにはWebアプリで共通の処理が用意されている（CreateViewは「作成」処理）
- 自分のWebアプリの項目を設定して使う（`form_class`, `template_name`）
- 追加の処理をさせたいときは、処理の一部を上書きする（`form_valid`）

+++

### ユーザ登録

- CreateViewでユーザを登録する
- 追加の処理をしないので上書きは不要。自分のアプリの項目を設定する

```python
from django.contrib.auth.forms import UserCreationForm
from django.urls import reverse_lazy
from django.views.generic import CreateView
class RegisterView(CreateView):
    template_name = 'accounts/register.html'
    form_class = UserCreationForm
    success_url = reverse_lazy('blog:post_list')
```

+++

TODO：コードの動作確認

@snap[west center]
```html
{% extends 'base.html' %}
{% block content %}
  <h2>Reader Registeration</h2>
  <form method="POST">
    {% csrf_token %}
    <table>
      {% for field in form %}
      <tr>
        <td>{{ field.label_tag }}</td>
        <td>{{ field }}</td>
      </tr>
      {% endfor %}
    </table>
    <input type="submit" value="register">
  </form>
{% endblock %}
```
@snapend

@snap[east center]
### RegisterViewの設定値
@ul[](false)
- 左は`template_name`に指定したテンプレートの例
- テンプレート中の`form`には、`form_class`に指定した[UserCreationForm](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.forms.UserCreationForm)が渡る
- 作成に成功すると、`success_url`に遷移する
@ulend
@snapend

+++

TODO：画面イメージ

---

### ユーザ管理までの道のり

1. クラスベースビュー
2. ユーザ作成（ジェネリックビュー）
3. **ユーザ管理（認証ビュー）**

+++

### 認証ビュー

- TODO：認証(Authentication)の定義（登録されたユーザであることを確認する）
- Djangoが認証のためのビューを用意している（`django.contrib.auth.views`）
- クラスベースビューで実装されている

+++

### 認証ビューの使用例：LoginView

- Extensions「[ウェブサイトをセキュアにする](https://tutorial-extensions.djangogirls.org/ja/authentication_authorization/)」で扱っている
- LoginViewをデフォルトの設定（`django.contrib.auth.views`に実装された設定）で使っている

+++

### LoginViewのデフォルト設定（一部）

- template_name：`registration/login.html`
  - そのため、`blog/templates/registration/login.html`を作った
- redirect_field_name：`next`
  - テンプレートで`<input type="hidden" name="next" value="{{ next }}" />`

[ドキュメント LoginView](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.views.LoginView)

+++

@snap[north span-100]
### 認証ビューの一覧
@snapend

@snap[west center]
@ul[](false)
- LoginView
- LogoutView
- PasswordChangeView（ログイン状態でパスワード変更）
- PasswordChangeDoneView
@ulend
@snapend

@snap[east center]
@ul[](false)
- PasswordResetView（「パスワードを忘れた場合」画面）
- PasswordResetDoneView
- PasswordResetConfirmView（メールで届くリンクからアクセスし、再設定）
- PasswordResetCompleteView
@ulend
@snapend

+++

### パスワード再設定

以下のようにビューを実装

```python
from django.contrib.auth.views import PasswordResetView

class PasswordReset(PasswordResetView):
    template_name = 'accounts/password_reset_form.html'
    success_url = reverse_lazy('accounts:password_reset_done')
    subject_template_name = 'accounts/mail_template/password_reset/subject.txt'
    email_template_name = 'accounts/mail_template/password_reset/message.html'
```

ref: naritoさんBlog [パスワード変更ページと忘れた際の再設定ページ](https://narito.ninja/blog/detail/44/)

+++

TODO：画面イメージ

+++

### [PasswordResetView](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.views.PasswordResetView)

- `template_name`のテンプレートを表示。Djangoに用意された[PasswordResetForm](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.forms.PasswordResetForm)が渡る
- 入力されたメールアドレスにメールを送る（件名には`subject_template_name`、本文はに`email_template_name`のテンプレートを使う）
- パスワード再設定のリクエストが処理されたら`success_url`に遷移する
- 注：機能させるにはユーザ登録でメールアドレスの入力を必須にする必要がある

---

### まとめ：ユーザまわりを実装

- もう一つのビューの書き方：クラスベースビュー
- Djangoに用意されたクラスベースビューを設定変更／処理の上書きをして使う
  - ジェネリックビュー
  - 認証ビュー
