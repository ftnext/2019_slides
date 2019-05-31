### Djangoでユーザ登録ハンズオン

- ハンズオンの準備をしよう
- **クラスベースビューを使ってみよう**
- ジェネリックビューを使ってみよう
- ユーザ登録機能を作ってみよう

+++

### クラスベースビューを使ってみよう

- クラスベースビューを紹介します
- 記事を作成するビュー（`post_new`）をクラスベースビューに書き換えてみます

---

### クラスベースビューを使ってみよう

- **クラスベースビューの紹介**
- クラスベースビューに書き換え

+++

### クラスベースビューの前に

Django Girls Tutorialで書いていたのは、**関数** ベースビュー

```python
# blog/views.pyから一部抜粋
def post_new(request):
    # 省略
```

>関数は def というキーワードからはじまり、（[Python入門](https://tutorial.djangogirls.org/ja/python_introduction/)より）

+++

### クラスベースビュー

- 「オブジェクト」としてビューを書く方法
- クラスベースビューを身につけると、Djangoに用意された機能を活用しやすい

+++

### クラスベースビュー

```python
class PostNew(View):
    # 省略
```

- `class`はオブジェクトを定義していることを表す
- `PostNew`はビューの名前
- `(View)`はPostNewがビューであるとDjangoが分かるようにしている

参考：[Django モデル](https://tutorial.djangogirls.org/ja/django_models/)

---

### クラスベースビューを使ってみよう

- クラスベースビューの紹介
- **クラスベースビューに書き換え**

+++

### 記事作成機能に関係するものを洗い出す

- モデル：Post
- URLConf；`path('post/new/', ..., name='post_new'),`
- ビュー：`post_new`
- テンプレート：blog/post_edit.html
  - フォーム：PostForm

+++

### クラスベースビューへの書き換え

1. URLConfを変更（クラスベースビュー用の書き方にする）
2. ビューをクラスベースビューで書く

今回は、モデル、テンプレート、フォームに変更はありません

+++

### ここからハンズオン本編です

- 一緒に手を動かしましょう（時間の関係でコピー&ペーストも使います）
- Tutorialにならって **エラーを出しながら** 進めます

---

### クラスベースビューへの書き換え

1. **URLConfを変更**（クラスベースビュー用の書き方にする）
2. ビューをクラスベースビューで書く

+++

### URLConf変更

`blog/urls.py`

```python
    # 変更前
    path('post/new/', views.post_new, name='post_new'),
    # 変更後
    path('post/new/', views.PostNew.as_view(), name='post_new'),
```

+++

### 動作確認：URLConf変更

一覧画面：http://127.0.0.1:8000/ にアクセス  
（スライドのリンクをクリックしてください）

+++

### エラー発生😱

- ブラウザでブログにアクセスできない
- コマンドラインを見る

>AttributeError: module 'blog.views' has no attribute 'PostNew'

+++

### エラーの原因

- エラーは、blog/views.pyにPostNewがないと言っている
- たしかに、まだ作成していない
- →解決策：blog/views.pyにPostNewビューを作ればよい

---

### クラスベースビューへの書き換え

1. URLConfを変更（クラスベースビュー用の書き方にする）
2. **ビューをクラスベースビューで書く**

まず最小限で簡単に作り、徐々に機能を追加していきます

+++

### はじめてのクラスベースビュー！

`blog/views.py`

```python
from django.views import View  # 追加

class PostNew(View):
    pass
```

+++

### はじめてのクラスベースビュー！

- クラスベースビューは、`class PostNew(View):`という書き方
  - 発展的な内容：Viewを「継承」したクラスを作っています
- `pass`により、現在のPostNewビューは何もしないビュー

+++

### 一覧画面 動作確認

http://127.0.0.1:8000/

- 書き方に問題はないので、先ほどのエラーは解決
- 一覧画面が表示される

+++

### 記事作成 動作確認

+のアイコンをクリックすると真っ白な画面に

![](django_girls_Jun_user_register_handson/assets/part2/1_no_post_new_form.png)

---

### 記事作成 フォーム表示

- 真っ白な画面に対処して、記事を作成するための画面（フォーム）を表示したい
- （フォームの機能はいったんは後回し。保存できなくてもよしとする）

+++

### クラスベースビューについてもう少し 1/2

- Webアプリにおける「ビュー」を **プロパティ** と **メソッド** をもつコードで表現
- これがオブジェクトでビューを書くということです

参考：[Django モデル](https://tutorial.djangogirls.org/ja/django_models/)

+++

### クラスベースビューについてもう少し 2/2

- プロパティ：状態（ビューの処理で参照される設定情報）
- メソッド：命令（ビューで行われる処理）

参考：[Django モデル](https://tutorial.djangogirls.org/ja/django_models/)

+++

### 記事作成 フォーム表示 1/2

クラスのプロパティを設定する

```python
class PostNew(View):
    # passとしていた部分を書き換える
    form_class = PostForm
    template_name = 'blog/post_edit.html'
```

まだ真っ白な画面です

+++

### 記事作成 フォーム表示 2/2

クラスにメソッドを追加

```python
class PostNew(View):
    form_class = PostForm
    template_name = 'blog/post_edit.html'

    # 以下を追加（form_class, template_nameと始まりの位置を揃えてください）
    def get(self, request, *args, **kwargs):
        form = self.form_class()
        return render(request, self.template_name, {'form': form})
```

+++

### フォーム表示 動作確認

- 一覧画面 http://127.0.0.1:8000/ にアクセス
- +のアイコンをクリックすると、フォームが表示される（やりました！）

+++

### フォームの保存を試みる

- 残念ながら保存できません（真っ白な画面再び）
- フォーム表示という目標は果たしたので、次はフォームから記事を保存できるようにします

+++

### 発展内容：HTTPメソッド

Webアプリへのデータの送り方は2通りある

- GET
- POST

URLに対してGETまたはPOSTでデータを送る

+++

### 発展内容：`get`

- GETメソッドでURLが呼び出された際の処理に対応
- URLのページを **ブラウザで単に表示** する際もGETメソッドを使う
- GETメソッドでデータを送ると、URLに含まれる

+++

### 解説：実は設定内容はこれまでと同じ

```python
# Tutorialの書き方（関数ベースビューと呼ばれる）
def post_new(request):
    if request.method == "POST":
        # 省略
    else:
        form = PostForm()
    return render(request, 'blog/post_edit.html', {'form': form})

# クラスベースビュー
def get(self, request, *args, **kwargs):
		form = self.form_class()  # form = PostForm()と同じ
		# render(request, 'blog/post_edit.html', {'form': form}) と同じ
		return render(request, self.template_name, {'form': form})
```

---

### 記事作成 1/2

クラスにメソッドを追加

```python
class PostNew(View):
    form_class = PostForm
    template_name = 'blog/post_edit.html'

    # getは変更がないので省略

    # 以下を追加（form_class, template_name, getと始まりの位置を揃えてください）
    def post(self, request, *args, **kwargs):
        form = self.form_class(request.POST)
        # このあと追加します
        return render(request, self.template_name, {'form': form})
```

+++

### 記事作成 2/2

```python
    def post(self, request, *args, **kwargs):
        form = self.form_class(request.POST)
        # 追加部分始まり（コピー&ペースト推奨）
        if form.is_valid():
            post = form.save(commit=False)
            post.author = request.user
            post.published_date = timezone.now()
            post.save()
            return redirect('post_list')
        # 追加部分終わり
        return render(request, self.template_name, {'form': form})
```

+++

### 動作確認

- 一覧画面 http://127.0.0.1:8000/
- フォームから保存できるようになりました

+++

### 発展内容：`post`

- POSTメソッドでURLが呼び出された際の処理に対応
- URLに含めずにデータを送る方法
- メリットの1つ：長いデータ（ブログの記事など）を送信できる

+++

### 解説：実は設定内容はこれまでと同じ

`if form.is_valid()`（フォームの入力内容に問題がない場合）の処理は全く同じなので省略

```python
# 関数ベースビュー
def post_new(request):
    if request.method == "POST":
        form = PostForm(request.POST)
        # 省略
    else:
        # 省略
    return render(request, 'blog/post_edit.html', {'form': form})

# クラスのベースビュー
def post(self, request, *args, **kwargs):
    # form = PostForm(request.POST)と同じ
    form = self.form_class(request.POST)
    # 省略
    return render(request, self.template_name, {'form': form})
```

---

### セキュリティ対応

- 書き換えの最後の1ステップが残っています
- 実は、今のままではログインしていないユーザも記事作成画面が見えちゃいます
- ログアウトしてから http://127.0.0.1:8000/post/new/ にアクセス

+++

### 記事の作成にはログインが必要とする

```python
from django.contrib.auth.mixins import LoginRequiredMixin  # 追加

class PostNew(LoginRequiredMixin, View):
    # この下に変更はありません
```

+++

### 記事の作成にはログインが必要とする

- ログインしたユーザのみ記事作成画面が見えるようにした
- 発展説明：Extensionsにある`@login_required`のクラスベースビュー版

+++

### 動作確認

ログアウトして http://127.0.0.1:8000/post/new/ にアクセス

![記事作成画面の表示にはログインが求められます](django_girls_Jun_user_register_handson/assets/part2/2_required_login.png)

---

### 小まとめ：クラスベースビュー

- urls.pyも変更が必要(`as_view()`)
- `class PostNew(View):`
- `get`, `post`というメソッドを用意しましょう
