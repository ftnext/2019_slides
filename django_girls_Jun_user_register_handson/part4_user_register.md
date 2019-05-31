### ユーザ登録機能を作ってみよう

ジェネリックビュー（`CreateView`）を使って、ユーザ登録機能を作成します

- 必要なものを整理
- 実際に作る

---

### ユーザ登録機能を作ってみよう

- **必要なものを整理**
- 実際に作る

+++

### 記事の作成で必要

- モデル：Post
- URLConf；`path('post/new/', ..., name='post_new'),`
- ビュー：`post_new`
- テンプレート：blog/post_edit.html
  - フォーム：PostForm

+++

### ユーザの作成に必要

- モデル
- URLConf
- ビュー
- テンプレート
  - フォーム

+++

### Djangoに用意されたものを使う

- **モデル**：User
- URLConf
- ビュー
- テンプレート
  - **フォーム**：UserCreationForm

+++

### 私たちで用意

- モデル
- **URLConf**
- **ビュー**
- **テンプレート**
  - フォーム

---

### ユーザ登録機能を作ってみよう

- 必要なものを整理
- **実際に作る**

+++

### ユーザ登録機能 作成手順

1. ユーザ管理用のアプリ作成
2. URLConf設定
3. CreateViewを使ってビューを用意
4. ユーザ登録用のテンプレートを用意

+++

### 1. アプリ作成

`python manage.py startapp accounts`

- ユーザ管理用のアプリaccountsを作る

+++

### Djangoのアプリケーション

- Djangoではアプリは機能ごとに作ることが多いです
- ブログの機能を担うblogアプリにユーザ管理機能をもたせるのは、私はオススメしません

（力試し：ハンズオンのあと、ログイン・ログアウトのURL設定もaccountsに移してみてください）

+++

### mysite/settings.py

アプリを「インストール」します

```python
INSTALLED_APPS = [
    'blog',
    'accounts',  # 追加
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

+++

### 2. URLConf設定

2つ設定します

- プロジェクトのURLConf
- アプリのURLConf

ユーザ登録画面を`http://127.0.0.1:8000/accounts/register/`とします

+++

### mysite/urls.py

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('accounts/login/', views.LoginView.as_view(), name='login'),
    path('accounts/logout/', views.LogoutView.as_view(next_page='post_list'), name='logout'),
    path('accounts/', include('accounts.urls')),  # 追加
    path('', include('blog.urls')),
]
```

+++

### accounts/urls.py（新規作成）

```python
from django.urls import path
from . import views

urlpatterns = [
    path('register/', views.Register.as_view(), name='register'),
]
```

+++

### 3. ビューを用意（accounts/views.py）

```python
from django.contrib.auth.forms import UserCreationForm
from django.urls import reverse_lazy
from django.views.generic import CreateView

class Register(CreateView):
    template_name = 'accounts/register.html'
    form_class = UserCreationForm
    success_url = reverse_lazy('post_list')
```

+++

### ビューの設定項目

TODO

CreateViewは変数の設定だけでよい（success_urlのreverse_lazy）

+++

### 4. ユーザ登録用のテンプレート

accounts/templates/accounts/register.html

TODO：エラーの表示は追加したほうがよい

```html
{% extends 'blog/base.html' %}

{% block content %}
    <h2>Reader Registeration</h2>
    <form method="POST">{% csrf_token %}
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

### 動作確認：ユーザ登録画面

http://127.0.0.1:8000/accounts/register/ にアクセスするとユーザ登録のフォームが表示される

![](django_girls_Jun_user_register_handson/assets/part4/1_user_registeration_form.png)

+++

ヘッダーにユーザ登録のアイコンを表示する

TODO：Glyphiconで人のアイコンを探す
