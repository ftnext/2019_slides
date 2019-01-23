### Appendix: 基本テンプレート

- post_list.htmlとpost_edit.htmlには共通部分が多い
- 例：見出しのDjango Girls Blog
- 共通部分＝繰り返されている

+++

### テンプレートの繰り返しをなくしたい

- 繰り返されていると保守性が低い
	- 見出しを変えることになったときに苦労する
	- 複数テンプレートを同じように編集😫
- そこで、基本テンプレートに共通化する

+++

### 基本テンプレート作成

- `blog/templates/blog/base.html`を作成
- 内容は次のスライド

+++

### 基本テンプレート base.html

```html
{% load static %}
<html>
    <head>
        <title>Django Girls blog</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <div class="page-header">
            {% if user.is_authenticated %}
                <a href="{% url 'post_new' %}" class="top-menu"><span class="glyphicon glyphicon-plus"></span></a>
            {% endif %}
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>

        <div class="content container">
            <div class="row">
                <div class="col-md-8">
                    {% block content %}
                    {% endblock %}
                </div>
            </div>
        </div>
    </body>
</html>
```

+++

### base.html

- headタグ（ブログアプリで使うCSSの設定）と見出しの部分を共通化
- `{% block content %}` `{% endblock %}`
	- この部分は各テンプレートの内容で置き換わる

+++

### post_list.html アップデート

まるまる以下のように書き換え

```html
{% extends 'blog/base.html' %}

{% block content %}
    {% for post in posts %}
        <div class="post">
            <div class="date">
                <p>published: {{ post.published_date }}</p>
            </div>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaksbr }}</p>
        </div>
    {% endfor %}
{% endblock %}
```

+++

### post_list.html アップデート

- 1行目`{% extends 'blog/base.html' %}`：基本テンプレートblog/base.htmlを使うと設定
- `{% block content %}`〜`{% endblock %}`：blog/base.htmlの`{% block content %}` `{% endblock %}`の部分を置き換える

+++

### 動作確認：ブログ記事を画面に表示する

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス
- テンプレートのファイルを変更したが、これまで同様、記事一覧が表示される

+++

### post_edit.html アップデート

まるまる以下のように書き換え

```html
{% extends 'blog/base.html' %}

{% block content %}
    {% for post in posts %}
        <h2>New post</h2>
        <form method="POST" class="post-form">{% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="save btn btn-default">Save</button>
        </form>
    {% endfor %}
{% endblock %}
```

+++

### 動作確認：フォームの表示

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス → 記事一覧が表示される
- 記事作成アイコン（リンク）をクリック → これまで同様、フォームが表示される

+++

### 基本テンプレート まとめ

- テンプレートで繰り返す部分をbase.htmlに共通化
- 保守性を高めた（変更しやすい）
	- 例えば、記事作成フォームへ遷移するリンクのアイコンを変える
	- base.htmlを修正するだけ（post_list.htmlやpost_edit.htmlは変更不要）
