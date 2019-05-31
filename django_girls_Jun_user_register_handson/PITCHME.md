## Djangoでユーザ登録ハンズオン
#### Django Girls Japan 勉強会(2019/06/01) nikkie

---

### 資料へのアクセス

勉強会の申し込みページ：https://djangogirls-org.connpass.com/event/131237/

資料にスライド・ソースコードのリンクがあります

+++

### 概要

- 5月のDjango Congressのトーク「[Django Girls Blogのネクストステップ](https://gitpitch.com/ftnext/2019_slides/master?p=django_congress_2019_blog_next_step)」の一部を再構成してハンズオン形式でお届けします
- Django Girls Tutorialから一歩進んで、ブログアプリにユーザ登録機能を追加します

+++

### お前、誰よ（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- Python歴1年半(2017/11頃〜) 、4月からデータサイエンティスト
- 2018/05~ [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/) 翻訳、Workshopコーチ
- 年に1度のPython祭り「PyCon JP」のスタッフ

---

### Webアプリって何よ？

- この勉強会に参加する際にconnpassというWebアプリを使っています
- ざっくり言うと、ブラウザから利用するアプリケーション

+++

### Webアプリは身近なので

- connpassにこんな機能あったらいいのに
- IT勉強会以外にも使えるconnpassみたいなアプリがあったらいいのに

※connpassはWebアプリの例です

+++

### Webアプリを作りたいあなたへ

- DjangoはWebアプリを作る方法の一つです
- Djangoを選ぶ場合、Djangoの使い方に加えて、Pythonというプログラミング言語を学ぶ必要があります

+++

### Djangoの学習と課題

- チュートリアル（[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)など）
- 課題：チュートリアルを終えても、作りたいアプリが作れるわけではない
- チュートリアルから次の一歩を踏み出すというテーマで5月に発表（その一部を、今回ハンズオンに）

---

### ハンズオンでやること

- Django Girls Tutorialのブログアプリに **ユーザ登録機能** を追加します
- Tutorialにはない「クラスベースビュー」「ジェネリックビュー」について説明します

+++

### ハンズオンで扱わないこと

- Congressの登壇の全てを扱うわけではありません
- Django Girls TutorialならびにExtensionsの内容は解説しません（終わった後にご確認ください）

+++

### アジェンダ

- ハンズオンの準備をしよう
- クラスベースビューを使ってみよう
- ジェネリックビューを使ってみよう
- ユーザ登録機能を作ってみよう

全て理解できなくても大丈夫です

---?include=django_girls_Jun_user_register_handson/part1_setup.md

---?include=django_girls_Jun_user_register_handson/part2_class_based_view.md

---?include=django_girls_Jun_user_register_handson/part3_generic_view.md

---?include=django_girls_Jun_user_register_handson/part4_user_register.md

---

### まとめ

- Tutorialとは別のビューの書き方：クラスベースビューを紹介
- ジェネリックビューの設定を変更して、記事作成機能、ユーザ登録機能を作成
- Djangoに用意された機能を利用する

+++

### ハンズオンの先のステップ

[5月の登壇資料](https://gitpitch.com/ftnext/2019_slides/master?p=django_congress_2019_blog_next_step)

- ユーザ登録でメールアドレスも入力させる
- ユーザのパスワード再設定の機能を提供（*認証ビュー*）

+++

### デモアプリ & サンプルコード

- [5月登壇の調査で作成したブログアプリ(PythonAnywhereにデプロイ)](https://ftnext.pythonanywhere.com/)
- [5月登壇資料に対応するソースコード](https://github.com/ftnext/nextstep_djangogirls_tutorial)

+++

### 書籍案内

- 『現場で使える Django の教科書』[基礎編](https://www.amazon.co.jp/dp/4802094744)・[実践編](https://www.amazon.co.jp/dp/B07L3DRGBT/)
- 『[基礎から学ぶ Django](https://www.amazon.co.jp/dp/486354247X/)』（期待を込めて）
- 『[プロになるためのWeb技術入門](https://www.amazon.co.jp/dp/4774142352)』（参考資料です。Webアプリについて知る）

+++

### スペシャルサンクス

- 勤務先のチームメンバー（練習協力ありがとうございます）
- Django Girls Japan勉強会運営の皆さま（機会をありがとうございます）

+++

### ご清聴ありがとうございました

ハンズオンお疲れさまでした！

Contact: [Twitter @ftnext](https://twitter.com/ftnext)／[匿名質問箱](https://peing.net/ja/ftnext)
