# 【エラーは友達】
# Django基礎ハンズオン
#### eLV勉強会 2019/01/24 nikkie

---

## Welcome to Django基礎ハンズオン

+++

## エラーは友達？

+++

私たち Django 仲良くなりたい

+++

Djangoの前にエラーが立ちはだかる 攻略できない。。

+++

このエラーと友達になることでDjangoとも仲良くなる

---

### ハンズオンを通して

- 一緒にエラーを出しながら解決策を学んでいく
- ハンズオンの後、「このエラーにはこうする」がわかる
- Djangoを使って作りたいものが作れる（に近づく）

+++

### ハンズオンの題材

- ブログアプリを作る
- ハンズオンは[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)に基づく

+++

### ブログアプリ作成手順

1. 管理画面からブログ記事を作る
2. ブログ記事を画面に表示する
3. ブログ画面からブログ記事を作る

+++

### 管理画面からブログ記事を作る

スクショ

+++

### ブログ記事を画面に表示する

スクショ

+++

### ブログ画面からブログ記事を作る

スクショ

---

### 自己紹介（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 3年目のソフトウェアエンジニア（Web開発、機械学習）
- 2018〜 Django Girls Tutorial翻訳に参加、Workshopコーチ

+++

### 注意事項

- 内容を絞ってDjango Girls Tutorialを一周します
	- ソースコードのコピペも行います
- 解説はDjangoに絞っています
	- Pythonの基礎、HTML、CSSについては詳しく取り上げません
- お手元のPCの中だけで動かします（今回はデプロイを扱いません）

+++

### ハンズオンを始める前に

1. コマンドライン（コマンドプロンプトやターミナル）を起動
2. errorfriendsディレクトリに移動する
	- 作成していない方は`mkdir errorfriends && cd errorfriends`
3. [環境構築参考記事](https://qiita.com/ftnext/items/082ec8fe96f26b181fc5)を参照された方は仮想環境を有効にする
	- Windows: `myvenv\Scripts\activate`
	- macOS: `source myvenv/bin/activate`

---?include=elv_Jan_django_errorfriends/part1.md

---?include=elv_Jan_django_errorfriends/part2.md

---?include=elv_Jan_django_errorfriends/part3.md

---

### まとめ

- ハンズオンでやったことの振り返り
- エラーへの対応
- ハンズオン後のDjangoの学び方案

+++

### 【エラーは友達】Django基礎ハンズオン

1. 管理画面からブログ記事を作る
2. ブログ記事を画面に表示する
3. ブログ画面からブログ記事を作る

+++

### エラーへの対応

- エラーは何が足りていないのかを示している
- AttributeError：views.pyに関数が用意されていない
- TemplateDoesNotExist：テンプレートが用意されていない
- NoReverseMatch：urlpatternsが設定されていない

+++

### Django機能開発チェックリスト

- [ ] 既存テンプレートに追加する画面へのリンクを追加したか
- [ ] 追加する画面用のurlpatternsを設定したか
- [ ] （追加する画面で使うモデルを設定したか）
- [ ] 追加する画面用のビュー関数を作成したか
- [ ] 追加する画面用のテンプレートを作成したか

漏れがある場合はエラーになる。そのエラーは解決できるはず

+++

冒頭 私たち Django 仲良くなりたい

+++

### 実はエラーはDjangoの一部

- エラーはDjangoの一部
- 友達になりたいのだから、エラーとうまくやっていける（はず）

+++

エラーはDjangoなのだからうまくやっていけるはず（敵ではない）

+++

### 力試し

1. 記事詳細画面追加
	- 記事一覧で記事のタイトルをクリックすると、記事の詳細が見られるようにしてください
	- 記事の詳細には「本文」「タイトル」「公開日」を表示してください
2. 記事編集画面追加
	- 記事詳細から記事編集フォームに遷移し、記事が変更できるようにしてください
	- PostFormを使って作成してください

+++

### ハンズオン後のDjangoの学び方案

- 力試しに取り組む
- または、[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)で復習（デプロイはスキップしてよい）
- [Django 投票アプリ チュートリアル](https://docs.djangoproject.com/ja/2.1/intro/tutorial01/)
- 参考：akiyokoさん [初学者・初級者向け Django の学習ロードマップ](https://akiyoko.hatenablog.jp/entry/2018/12/01/133427)

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
2月に続編の勉強会を開催予定です。
