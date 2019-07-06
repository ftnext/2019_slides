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

[ソースコード tag:2-user_management](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/2-user_management)

---

### ユーザ管理までの道のり

1. **クラスベースビュー**
2. ユーザ作成（ジェネリックビュー）
3. ユーザ管理（認証ビュー）

[ソースコード tag:2-user_management](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/2-user_management)

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
- クラスを使って書く **クラスベース** ビューを紹介（class based view）
- 次のスライドで、post_newビューを書き換えます

+++?code=django_congress_2019_blog_next_step/src/part2/PostNew_CBV.py&lang=python&title=Example of Class Based View

+++

### クラスベースビュー

- Djangoに用意されたビューのクラスを継承（例では`django.views.View` [docs](https://docs.djangoproject.com/ja/2.2/ref/class-based-views/base/)）
- 継承元のクラスに定義された変数や関数のうち必要なものを更新して使う
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

[ソースコード tag:2-user_management](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/2-user_management)

+++

### ジェネリックビュー

- どんなWebアプリでも使う共通処理がある
  - 例：データベースのデータの **一覧、作成** など
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
    form_class = PostForm  # テンプレートにformとして渡る
    template_name = 'blog/post_edit.html'  # テンプレートの指定

    def form_valid(self, form):
        # 入力値に問題がない場合に呼ばれる処理
        # authorの設定追加のために上書き
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

### CreateView設定項目（ビュー以外）

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
- 今回は追加の処理をしない（上書き不要）。自分のアプリの項目を設定する

```python
from django.contrib.auth.forms import UserCreationForm
from django.urls import reverse_lazy
from django.views.generic import CreateView
class Register(CreateView):
    template_name = 'accounts/register.html'
    form_class = UserCreationForm
    success_url = reverse_lazy('blog:post_list')
```

ref:『[Building Django 2.0 Web Application](https://www.amazon.co.jp/dp/B079DW6TRJ)』

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

[ソースコード tag:2-user_management](https://github.com/ftnext/nextstep_djangogirls_tutorial/releases/tag/2-user_management)

+++

### 認証ビュー

- 認証(Authentication)して、登録されたユーザであることを確認する
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

### その他の認証ビュー

- LoginView以外にも認証ビューは用意されている
- Webアプリのユーザまわり（パスワードまわり）でよく使う機能
- 画面例を表示します

+++

@snap[west span-50 text-center]
### パスワード変更
![ログインしているユーザは自身のパスワードを変更できます](django_congress_2019_blog_next_step/assets/part2/2_change_password.png)
@snapend

@snap[east span-50 text-center]
### パスワード変更完了
![](django_congress_2019_blog_next_step/assets/part2/3_change_password_done.png)
@snapend

+++

@snap[west span-50 text-center]
### パスワード再設定リクエスト
![パスワードを忘れた場合、メールアドレスを入力します](django_congress_2019_blog_next_step/assets/part2/4_reset_password_request.png)
@snapend

@snap[east span-50 text-center]
### 再設定用のメール送信完了
![入力したメールアドレスにパスワード再設定画面のリンクがメールで届きます](django_congress_2019_blog_next_step/assets/part2/5_password_reset_mail_done.png)
@snapend

+++

@snap[west span-50 text-center]
### パスワード再設定（メールからアクセス）
![パスワードを再設定する画面です](django_congress_2019_blog_next_step/assets/part2/6_password_reset.png)
@snapend

@snap[east span-50 text-center]
### パスワード再設定完了
![](django_congress_2019_blog_next_step/assets/part2/7_password_reset_complete.png)
@snapend

+++

@snap[north span-100]
### 認証ビューの一覧
@snapend

@snap[west span-45 text-center]
@ul[](false)
- LoginView
- LogoutView
- PasswordChangeView（ログイン状態でパスワード変更）
- PasswordChangeDoneView
@ulend
@snapend

@snap[east span-45 text-center]
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
from django.contrib.auth.forms import PasswordResetForm
from django.contrib.auth.views import PasswordResetView

class PasswordReset(PasswordResetView):
    subject_template_name = 'accounts/mail_template/password_reset/subject.txt'
    email_template_name = 'accounts/mail_template/password_reset/message.html'
    template_name = 'accounts/password_reset_form.html'
    form_class = PasswordResetForm
    success_url = reverse_lazy('accounts:password_reset_done')
```

ref: naritoさんBlog [パスワード変更ページと忘れた際の再設定ページ](https://narito.ninja/blog/detail/44/)

+++

### [PasswordResetView](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.views.PasswordResetView) 1/2

ユーザ登録の時と同様、**設定をしている** にすぎない

設定項目 | 内容
----- | -----
`template_name` | 表示するテンプレート
`form_class` | テンプレートに渡るフォーム。<br>Djangoに用意された[PasswordResetForm](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.forms.PasswordResetForm)を指定

+++

### [PasswordResetView](https://docs.djangoproject.com/ja/2.2/topics/auth/default/#django.contrib.auth.views.PasswordResetView) 2/2

設定項目 | 内容
----- | -----
`subject_template_name` | 送るメールの件名を書いたファイル
`email_template_name` | 送るメールの本文を書いたファイル
`success_url` | パスワード再設定のリクエストが処理されたら遷移

+++

### こんなメールが届きます

![](django_congress_2019_blog_next_step/assets/part2/reset_mail.png)

+++

### 注：パスワード再設定を機能させるために

- ユーザ登録でメールアドレスの入力を必須にする必要がある
- UserCreationFormをカスタマイズし、`form_class`に設定する

+++

### accounts/forms.py

```python
from django import forms
from django.contrib.auth import get_user_model
from django.contrib.auth.forms import UserCreationForm
from django.utils.translation import ugettext_lazy as _

User = get_user_model()

class MyRegisterForm(UserCreationForm):
    email = forms.EmailField(label=_("Email"), required=True)

    class Meta:
        model = User
        fields = ('username', 'email',)

    # Bootstrapのクラス設定やEメールの重複があると登録エラーとする処理を省略しています
```

+++

### ユーザ登録にメールアドレスを追加

![](django_congress_2019_blog_next_step/assets/part2/8_user_register_add_email.png)

---

### まとめ：ユーザまわりを実装

- もう一つのビューの書き方：クラスベースビュー
- Djangoに用意されたクラスベースビューを設定変更／処理の上書きをして使う
  - ジェネリックビュー
  - 認証ビュー
- 手を動かしたい方へ：[6月に開催したハンズオン](https://gitpitch.com/ftnext/2019_slides/master?p=django_girls_Jun_user_register_handson)

+++

### 参考：さらに進んだ認証

「[Django における認証処理実装パターン](https://nwpct1.hatenablog.com/entry/django-auth-patterns)」  
DjangoCongress 2018 c-bataさん

- ユーザ名の代わりにメールアドレスを使った認証
- OAuth（Googleアカウントなどでログイン）
