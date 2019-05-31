### Djangoでユーザ登録ハンズオン

- ハンズオンの準備をしよう
- クラスベースビューを使ってみよう
- **ジェネリックビューを使ってみよう**
- ユーザ登録機能を作ってみよう

+++

### ジェネリックビューを使ってみよう

- ジェネリックビュー（＝汎用ビュー）を紹介します
- クラスベースビュー`PostNew`をジェネリックビューを使って書き換えてみます

---

### ジェネリックビューを使ってみよう

- **ジェネリックビューの紹介**
- ジェネリックビューに書き換え

+++

### Webアプリの処理

- Webアプリに共通する処理がある
- 例えば、何かを新規に作成する処理

+++

### ジェネリックビューとは？

- Webアプリの共通処理を担うビュー
- Djangoに用意されていて、クラスベースビューで書かれている
- 日本語ドキュメントでは「汎用ビュー」

+++

### ジェネリックビュー 一覧

- 表示系：一覧、詳細
- 編集系：作成、更新、削除
- アーカイブ系：年・月・週などの単位

[ビルトインのクラスベースビュー API](https://docs.djangoproject.com/ja/2.2/ref/class-based-views/)

+++

### ジェネリックビューの使い方

- ジェネリックビューは抽象的な処理を表す（例；「何か」を作成）
- 自分のWebアプリ向けに設定して使う（例：記事を作成）

---

### ジェネリックビューを使ってみよう

- ジェネリックビューの紹介
- **ジェネリックビューに書き換え**

+++

### ジェネリックビューへの書き換え

1. ビューをジェネリックビューで書く

今回は、URLConf、モデル、テンプレート、フォームに変更はありません

+++

### blog/views.py

```python
# from django.views import View  # 使わないので削除
from django.urls import reverse_lazy  # 追加
from django.views.generic import CreateView  # 追加

class PostNew(LoginRequiredMixin, CreateView):
    form_class = PostForm
    template_name = 'blog/post_edit.html'
    success_url = reverse_lazy('post_list')
```

+++

### CreateView 設定項目

- `form_class`：表示するフォームを指定
- `template_name`：テンプレートを指定
- `success_url`：作成完了後に表示するURLを指定（`path()`の`name`で指定）

[クラスベース汎用ビュー - フラットインデックス CreateView](https://docs.djangoproject.com/ja/2.2/ref/class-based-views/flattened-index/#createview)

+++

### 動作確認

- 作成画面 http://127.0.0.1:8000/post/new/
- フォームの表示はされます
- 保存してみると。。。

+++

### 保存すると、エラー発生😱

![](django_girls_Jun_user_register_handson/assets/part3/1_not_exist_form_valid.png)

設定されているべきauthorが設定されていないためエラー

+++

### 発展内容：CreateView

- CreateViewの中にgetとpostメソッドが用意されている
- `myvenv/lib/python3.7/site-packages/django/views/generic/edit.py` で確認できる（次スライド）

+++

### 発展内容：CreateView

```python
class BaseCreateView(ModelFormMixin, ProcessFormView):
    """
    Base view for creating a new object instance.

    Using this base class requires subclassing to provide a response mixin.
    """
    def get(self, request, *args, **kwargs):
        self.object = None
        return super().get(request, *args, **kwargs)

    def post(self, request, *args, **kwargs):
        self.object = None
        return super().post(request, *args, **kwargs)


class CreateView(SingleObjectTemplateResponseMixin, BaseCreateView):
    """
    View for creating a new object, with a response rendered by a template.
    """
    template_name_suffix = '_form'
```

---

### 記事を保存する際の設定を追加

- フォームで入力されないauthorを追加する
- 一覧画面に記事を表示するためにpublished_dateを設定する

+++

### 記事を保存する際の設定を追加

```python
class PostNew(LoginRequiredMixin, CreateView):
    # プロパティの設定は省略（変更なし）

    # フォームの入力内容に問題がない場合の処理をカスタマイズ
    def form_valid(self, form):
        form.instance.author = self.request.user
        form.instance.published_date = timezone.now()
        return super().form_valid(form)
```

+++

### 動作確認

- 作成画面 http://127.0.0.1:8000/post/new/
- 記事を保存できます！

+++

### やや発展：`form_valid`メソッド

- `post`ではなく`form_valid`メソッドを定義した
- これはCreateViewの`post`メソッドで呼び出されるメソッド
- ブログアプリ用に **上書き設定** した（`post`をまるまる定義しなくてよい）

参考：[Models and request.user](https://docs.djangoproject.com/ja/2.2/topics/class-based-views/generic-editing/#models-and-request-user)

---

### 小まとめ：ジェネリックビュー

- Djangoに用意されたクラスベースビュー
- クラスベースビューで書くよりも簡単に書ける
- プロパティやメソッドを自分のアプリ用に設定して使う
