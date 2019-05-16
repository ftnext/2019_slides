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

### Tutorialで書くビュー

[テンプレート内の動的データ](https://tutorial.djangogirls.org/ja/dynamic_data_in_templates/)

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

+++

### Djangoのビューの書き方は2通り

- Django Girls Tutorialで書いてきたビューは **関数ベース** ビュー
- クラスを使って書く **クラスベース** ビューを紹介
- 次のスライドで、post_newビューを書き換えます

+++?code=django_congress_2019_blog_next_step/src/part2/PostNew_CBV.py&lang=python&title=Example of Class Based View

+++

### クラスベースビュー

- Djangoに用意されたビューのクラスを継承（例では`django.views.View`）
- クラスの属性（attribute。元のクラスに定義された変数や関数）を更新して使う
- urls.pyでは`as_view()`を使ってpathを書く

```python
    path('post/new/', views.PostNew.as_view(), name='post_new'),
```

+++

### 2つの違い

関数ベースビュー | クラスベースビュー
----- | -----
`request.method == 'POST'`という条件分岐 | `get`, `post`というHTTPメソッドに対応するメソッドを定義

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

+++?code=django_congress_2019_blog_next_step/src/part2/PostNew_CBV.py&lang=python&title=Before: Class Based View

+++

### After: CreateView (GenericView)

```python
# CreateViewを使って書き換え
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import CreateView
from .forms import PostForm

class PostNew(LoginRequiredMixin, CreateView):
    form_class = PostForm
    template_name = 'blog/post_edit.html'

    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)
```

ref: [Models and request.user](https://docs.djangoproject.com/ja/2.2/topics/class-based-views/generic-editing/#models-and-request-user)

+++

### ジェネリックビューを使う

- ジェネリックビューにはWebアプリで共通の処理が用意されている（CreateViewは「作成」処理）
- 自分のWebアプリの項目を設定して使う（`form_class`, `template_name`）
- 追加の処理をさせたいときは、処理の一部を上書きする（`form_valid`）

+++

### CreateView設定項目 1/2

- `template_name`に指定されたテンプレートを使う
- `form_class`に指定されたフォームを`form`として渡す
- 入力値に問題がないときの処理`form_valid`にauthorの設定を追加

+++

### CreateView設定項目 2/2

- 作成後、記事の詳細画面に遷移するという動作は変えない
- 作成された記事のURLを取得するメソッドをPostモデルにメソッドを追加（記事作成後に呼び出される）

```python
from django.urls import reverse
class Post(models.Model):
    # : (省略)
    def get_absolute_url(self):
        return reverse('blog:post_detail', kwargs={'pk': self.pk})
```

ref: [モデルフォーム](https://docs.djangoproject.com/ja/2.2/topics/class-based-views/generic-editing/#model-forms)

+++

### ユーザ登録

- CreateViewでユーザを登録する
- 追加の処理をしないので、処理の上書きは不要。自分のアプリの項目を設定する

```python
from django.contrib.auth.forms import UserCreationForm
from django.urls import reverse_lazy
from django.views.generic import CreateView
class Register(CreateView):
    template_name = 'accounts/register.html'
    form_class = UserCreationForm
    success_url = reverse_lazy('blog:post_list')
```

ref:『[Building Django 2.0 Web Application](https://www.amazon.co.jp/dp/B079DW6TRJ)）』

+++

### ユーザ登録テンプレート

`accounts/register.html`

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

+++

### Registerの設定値

- 前のスライドで示したテンプレートを`template_name`に指定
- テンプレート中の`form`には、`form_class`に指定した[UserCreationForm](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.forms.UserCreationForm)が渡る
- 作成に成功すると、`success_url`（記事一覧）に遷移する

+++

### ユーザ登録

![ユーザ名とパスワードをフォームから設定します](django_congress_2019_blog_next_step/assets/part2/1_register_user.png)

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
