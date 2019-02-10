### 【羅針盤を手に入れる】<br>Django基礎ハンズオンⅡ

0. <div class="django-girls-highlight">ブログアプリの機能のおさらい（10分）</div>
1. ブログ画面からブログ記事を作る（40分）
2. ブログ記事の詳細が見られるようにする（30分）
3. ブログ記事に画像を追加できるようにする（30分）

+++

### ブログアプリの機能のおさらい

- 準備：機能を確認する前に
- 機能1：管理画面からブログ記事を作れる
- 機能2：ブログ記事を一覧に表示する

+++

### 機能を確認する前に

1. 開発に使うものを整理
2. データベースの用意
3. 管理画面にログインするユーザ作成

+++

### (1)開発に使うものを整理

- A) エディタ
- B) コマンドライン
- C) ブラウザ

+++

### A) エディタ

- 例：Visual Studio Code, Atom, ...（お好みで）
- 用途：@color[#ff9400](ファイルの編集)
- PythonのコードやHTMLを書く

+++

### フォルダ構造を見ながらがオススメ

![エクスプローラーやFinderを使わなくてもエディタからファイルやフォルダを作れます](elv_Feb_django_developcompass/assets/part0/vscode_operate_files.png)

+++

### B) コマンドライン

- 例：コマンドプロンプト(Windows)、ターミナル(Mac)
- 用途：@color[#ff9400](コマンドの実行)
- @color[#ff9400](エラーが表示される)場所でもある

+++

### コマンドで行うこと（一例）

Djangoに用意されたコマンドを使って開発を進める

- 必要なファイルを作成 startapp
- データベース操作 migrate
- Webアプリを動かす runserver

+++

### C) ブラウザ

- 例：Google Chrome, ...（お好みで）
- 用途：@color[#ff9400](Webアプリの動作確認)
- 一部エラーが表示される

+++

### 開発に使うもの

- エディタ：PythonやHTMLを書く
- コマンドライン：Djangoに用意されたコマンドを使う
- ブラウザ：動作確認

+++

### (2)データベースの用意

- コマンドラインで以下を入力
  - `python manage.py migrate`
  - ブログアプリが使うデータベースの初期設定

+++

### (3)管理画面にログインするユーザ作成

- コマンドラインで`python manage.py createsuperuser`
	- ユーザ名
	- メールアドレス
	- パスワード

+++

### サーバを起動

- コマンドラインで`python manage.py runserver`
  - サーバを起動するとブラウザでブログアプリにアクセスできる
  - 止め方：コマンドラインでCtrlキーとCキーを同時押し

+++

### 管理画面にログイン

- ブラウザでアクセス http://127.0.0.1:8000/admin/
- 先ほど作ったユーザでログイン（ユーザ名とパスワード）

+++

### 管理画面にログイン

![このあとは管理画面から記事を作成します](elv_Jan_django_errorfriends/assets/part1/2_admin.png)

---

### 機能1：管理画面からブログ記事を作れる

- ログイン後の画面にてPostsを「追加」
- フォームに入力する

+++

### 記事の項目（5つ）1/2

Postモデルでの名前 | 意味するもの | 備考
----- | ----- | -----
author | 作成者 |  Djangoが用意したUserモデルと紐づけ
title | ブログタイトル | 200文字以下の文字列
text | ブログ本文 | 大量の文字列（複数行に渡って書ける）

+++

### 記事の項目（5つ）2/2

Postモデルでの名前 | 意味するもの | 備考
----- | ----- | -----
created_date | 作成日 | 日付
published_date | 公開日 | 日付

+++

### フォーム入力

<span class="sixty-percent-img">
![管理画面から記事を作る](elv_Jan_django_errorfriends/assets/part1/3_add_post.png)
</span>

+++

### 記事をいくつか作ってみましょう

今回から参加された方向け

- 公開日を設定した記事を1つ
- 公開日を設定しない記事を1つ

+++

### 管理画面から記事を作るための設定内容

- blog/models.py：ブログ記事の項目
- blog/admin.py：管理画面から記事を作れるよう設定
- @color[#ff9400](残りはDjangoに用意)されている

---

### 機能2：ブログ記事を一覧に表示する

<span class="sixty-percent-img">
![CSS設定済みブログ一覧](elv_Jan_django_errorfriends/assets/part2/3_post_list_with_style.png)
</span>

+++

### ブログ一覧画面にアクセス

- Ctrl+Cで止めている場合、コマンドラインで`python manage.py runserver`
- ブラウザで http://127.0.0.1:8000/ にアクセス

+++

### ブログ一覧機能

- @color[#ff9400](公開日が設定されている記事)を表示
- 最近公開されたものが上に並ぶ
- 記事は公開日、タイトル、本文が表示される

+++

### ブログ一覧のための設定内容

- blog/urls.py：URLの設定
- blog/views.py：ビュー（どのデータを見せるか）
- blog/templates/blog/post_list.html：テンプレート（表示の仕方）

+++

### Djangoの動き

![URLに対応するビューが呼び出され、必要なモデルにアクセス、取得した結果をテンプレートに埋め込み、HTMLを生成して返す](elv_Feb_django_developcompass/assets/part0/django_structure.001.png)

+++

### URL設定 → ビュー

![URLに対応するビューが呼び出される部分について](elv_Feb_django_developcompass/assets/part0/django_structure.002.png)

+++

### URL設定 → ビュー

- URLのパスの部分とビューの関数を対応付ける
  - パス`''`（URL：http://127.0.0.1:8000/ ）へのアクセスは、blog/views.pyの`post_list`関数を呼び出す
- 大元のURLの設定（mysite/urls.py）がblog/urls.pyのURL設定を読み込むように設定

+++

### URLの例：http://www.example.com/index

- `http`：プロトコル
- `www.example.com`：ホスト（インターネット上のコンピュータ）
- `index`：@color[#ff9400](パス)（サーバ上のどこにアクセスするかの指定）

+++

### ビュー・モデル・テンプレート

![ビューがモデルにアクセスし、取得した結果をテンプレートに埋め込み、HTMLを生成する部分について](elv_Feb_django_developcompass/assets/part0/django_structure.003.png)

+++

### ビュー：`post_list`関数の行う処理

ユーザが見るのはどのデータかを指定（ブログの一覧）

1. 公開日時が設定された記事をモデルから取得
2. テンプレートに記事のデータを埋め込んで表示する

+++

### テンプレート

- 表示の仕方をHTMLで書く
- HTMLタグの他にもタグが書ける
  - `{% %}`：for文やif文などが書ける
  - `{{ }}`：変数の値に置き換わる

+++

### 一覧画面のテンプレート：blog/post_list.html

- 取得した記事の一覧がpostsという変数で渡る
- `{% for %}`で記事の一つ一つを取り出して処理
- 例えば`{{ post.title }}`は記事のタイトルに置き換わる

+++

### ポイント：ブログアプリの機能のおさらい

- エディタ・コマンドライン・ブラウザを使って開発
- Djangoの動き：URL・モデル・ビュー・テンプレート
