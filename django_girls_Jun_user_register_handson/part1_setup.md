### Djangoでユーザ登録ハンズオン

- **ハンズオンの準備をしよう**
- クラスベースビューを使ってみよう
- ジェネリックビューを使ってみよう
- ユーザ登録機能を作ってみよう

+++

### ハンズオンの準備をしよう

- 開発に必要なものを整える
- ブログアプリが動くようにする
- ブログアプリを触ってみる

---

### ハンズオンの準備をしよう

- **開発に必要なものを整える**
- ブログアプリが動くようにする
- ブログアプリを触ってみる

+++

### 開発に必要なものを整える

- Pythonのインストール
- エディタ(Atom)のインストール
- ハンズオンのソースコードをダウンロード

+++

### Pythonのインストール

Django Girls Tutorial [Pythonをはじめよう](https://tutorial.djangogirls.org/ja/python_installation/)

+++

### Atomのインストール

Django Girls Tutorial [コードエディタ](https://tutorial.djangogirls.org/ja/code_editor/)

+++

### ソースコードダウンロード

https://github.com/ftnext/djangogirls-user-register

「Clone or download」から「Download ZIP」

+++

### ソースコードの配置

- ZIP形式でダウンロードしたソースコードを展開
- 展開されたディレクトリの名前を`user_register`と変更
- `user_register`をホームディレクトリに置きましょう（口頭で補足）

---

### ハンズオンの準備をしよう

- 開発に必要なものを整える
- **ブログアプリが動くようにする**
- ブログアプリを触ってみる

+++

### ブログアプリが動くようにする

- コマンドラインでいくつかコマンドを入力します
- Windowsの方はコマンドプロンプトを、Macの方はターミナルを起動してください
- 最初のコマンド：`cd user_register`

+++

### 仮想環境作成（Windows編）

Django Girls Tutorial [Djangoのインストール](https://tutorial.djangogirls.org/ja/django_installation/)

```shell
python -m venv myvenv
myvenv\Scripts\activate
```

+++

### 仮想環境作成（macOS編）

Django Girls Tutorial [Djangoのインストール](https://tutorial.djangogirls.org/ja/django_installation/)

```shell
python3 -m venv myvenv
source myvenv/bin/activate
```

+++

### Djangoのインストール

Django Girls Tutorial [Djangoのインストール](https://tutorial.djangogirls.org/ja/django_installation/)

```shell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

+++

### ソースコードを動かす

```shell
# データベースのセットアップ
python manage.py migrate
# スーパーユーザの作成
python manage.py createsuperuser
# サーバの起動
python manage.py runserver
```

---

### ハンズオンの準備をしよう

- 開発に必要なものを整える
- ブログアプリが動くようにする
- **ブログアプリを触ってみる**

+++

### 配布したブログアプリの機能

- ブログ記事の一覧
- ブログ記事の作成
- ログイン・ログアウト

一通り触ってみます

+++

### Adminにログイン

次のリンクをクリック：http://127.0.0.1:8000/admin

先ほど設定したユーザ名とパスワードでログインしてください

+++

### 記事を作る（公開日設定）

<span class="seventy-percent-img">
![](django_girls_Jun_user_register_handson/assets/part1/1_post_published.png)
</span>

+++

### one more（公開日未設定）

<span class="seventy-percent-img">
![](django_girls_Jun_user_register_handson/assets/part1/2_post_not_published.png)
</span>

+++

### サイトを表示する

![](django_girls_Jun_user_register_handson/assets/part1/3_see_site.png)

+++

### 表示したサイト＝記事一覧

![](django_girls_Jun_user_register_handson/assets/part1/35_post_list.png)

+++

### ブログ記事の一覧

- 現在より前の日時で公開日が設定されている記事が表示されます
- 公開日が設定されていない記事は表示されていません

+++

### サイトのフォームから記事を作る

![](django_girls_Jun_user_register_handson/assets/part1/4_post_new_form.png)

+++

### フォームから作った記事は、公開日が設定されます

![](django_girls_Jun_user_register_handson/assets/part1/5_post_published_form.png)

+++

### サイトからログアウト

![](django_girls_Jun_user_register_handson/assets/part1/6_logout.png)

+++

### サイトにログイン

![](django_girls_Jun_user_register_handson/assets/part1/7_login.png)

---

### 最後に、Atomでソースコードを開く

File → Open からホームディレクトリの`user_register`を開く

![左側を操作するとファイルが開けるので便利です](django_girls_Jun_user_register_handson/assets/part1/8_atom.png)

+++

### 以上で、準備完了です！
