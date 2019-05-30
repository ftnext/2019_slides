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

- Webアプリの共通処理をDjangoが用意している
- クラスベースビューで書かれている
- 日本語ドキュメントでは「汎用ビュー」

+++

### ジェネリックビュー

TODO：一覧を示す

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

### 動作確認

これだけでフォームの表示はされる。

+++

### ジェネリックビュー

- CreateViewの中にgetとpostメソッドが用意されている
getやpostでフォームを表示する際のフォーム、テンプレートの設定

メモ：保存に成功した場合の遷移先の設定が必要（リダイレクト先が不明のエラー）
>No URL to redirect to.  Either provide a url or define a get_absolute_url method on the Model.

---

保存する際の設定が必要（著者の部分）

+++

```python
class PostNew(LoginRequiredMixin, CreateView):
    # プロパティの設定は省略（変更なし）

    # フォームの入力内容に問題がない場合の処理をカスタマイズ
    def form_valid(self, form):
        form.instance.author = self.request.user
        form.instance.published_date = timezone.now()
        return super().form_valid(form)
```

Djangoが用意している一連の処理の中のform_validを上書き
（TODO：一連の処理はもう少し具体的に示したい）

+++

ジェネリックビューを使うとクラスベースビューを簡単にかけることを学んだ
