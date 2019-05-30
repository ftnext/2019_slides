## ユーザ登録（TODO：要ブラッシュアップ）

CreateViewを使う
ユーザ登録のフォームはDjangoが用意しているUserCreationFormを使う

+++

ユーザ管理用のアプリ（accountsを作る。アプリは機能ごとに作る）
`python manage.py startapp accounts`

（力試し：ハンズオンのあと、ログイン・ログアウトのURL設定もaccountsに移してみてください）

+++

### mysite/settings.py

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

### accounts/views.py

```python
from django.contrib.auth.forms import UserCreationForm
from django.urls import reverse_lazy
from django.views.generic import CreateView

class Register(CreateView):
    template_name = 'accounts/register.html'
    form_class = UserCreationForm
    success_url = reverse_lazy('post_list')
```

CreateViewは変数の設定だけでよい（success_urlのreverse_lazy）

+++

### accounts/templates/accounts/register.html

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

http://127.0.0.1:8000/accounts/register/ にアクセスするとユーザ登録のフォームが表示される

![](django_girls_Jun_user_register_handson/assets/part4/1_user_registeration_form.png)

+++

ヘッダーにユーザ登録のアイコンを表示する

TODO：Glyphiconで人のアイコンを探す
