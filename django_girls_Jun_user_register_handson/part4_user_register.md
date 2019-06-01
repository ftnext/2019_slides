### Djangoでユーザ登録ハンズオン

- ハンズオンの準備をしよう
- クラスベースビューを使ってみよう
- ジェネリックビューを使ってみよう
- **ユーザ登録機能を作ってみよう**

+++

### ユーザ登録機能を作ってみよう

ジェネリックビュー（`CreateView`）を使って、ユーザ登録機能を作成します

- 必要なものを整理
- 実際に作る

---

### ユーザ登録機能を作ってみよう

- **必要なものを整理**
- 実際に作る

+++

### 記事の作成で必要だった

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

1. ユーザ管理用のアプリケーション作成
2. URLConf設定
3. CreateViewを使ってビューを用意
4. ユーザ登録用のテンプレートを用意

+++

### 1. アプリケーション作成

ユーザ管理用のアプリケーションaccountsを作る

1. コマンドラインで CtrlキーとCキーを同時押し（runserverを終了）
2. `python manage.py startapp accounts`

+++

### Djangoのアプリケーション

- Djangoではアプリケーションは機能ごとに作ることが多いです
- ブログの機能を担うblogアプリケーションにユーザ管理機能をもたせるのは、私はオススメしません

（力試し：ハンズオンのあと、ログイン・ログアウトのURL設定もaccountsに移してみてください）

+++

### mysite/settings.py

アプリケーションを「インストール」します

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
- アプリケーションのURLConf

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

### 4. ユーザ登録用のテンプレート

accounts/templates/accounts/register.html

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
                    <td>{{ field.errors }}</td>
                </tr>
            {% endfor %}
        </table>
        <input type="submit" value="register">
    </form>
{% endblock %}
```

+++

### 動作確認：ユーザ登録機能

1. コマンドラインで`python manage.py runserver`
2. http://127.0.0.1:8000/accounts/register/ にアクセスする

+++

### ユーザ登録できます！

![](django_girls_Jun_user_register_handson/assets/part4/1_user_registeration_form.png)

+++

### ヘッダーにユーザ登録へのリンクを追加

blog/templates/blog/base.html

```html
<div class="page-header">
    {% if user.is_authenticated %}
        <!-- 変更なし。省略 -->
    {% else %}
        <a href="{% url 'login' %}" class="top-menu"><span class="glyphicon glyphicon-lock"></span></a>
        <!-- 以下の1行を追加 -->
        <a href="{% url 'register' %}" class="top-menu"><span class="glyphicon glyphicon-user"></span></a>
    {% endif %}
    <h1><a href="/">Django Girls Blog</a></h1>
</div>
```

---

### 小まとめ：ユーザ登録機能

- ユーザ管理用のアプリケーションを作成
- モデルとフォームはDjangoが用意したものを使用
- URLConf、ビュー、テンプレートを用意
