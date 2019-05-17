## Django Girls Blogのネクストステップ
## 〜実務レベルへ橋渡し〜
#### Django Congress 2019 nikkie

---

### Dedication（献辞）

やりたいことに取り組むことをいつも応援してくれる両親に本発表を捧げます。

〜 Mother's Day & Father's Day 〜

+++

### お前、誰よ（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- Python歴1年半(2017/11頃〜) 実務ではWeb開発(Flask)、機械学習
- 2018/05~ [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/) 翻訳、Workshopコーチ
- Django Girls Tutorialをベースにしたハンズオン開催 [2019/01](https://gitpitch.com/ftnext/2019_slides/master?p=elv_Jan_django_errorfriends/), [2019/02](https://gitpitch.com/ftnext/2019_slides/master?p=elv_Feb_django_developcompass/)

+++

### アンケート

1. Django Girls Tutorialに取り組んだことのある方🙋‍
2. 実務や個人開発でDjangoを使っている方🙋‍

---

### Django Girls Workshop

- [Tutorial](https://tutorial.djangogirls.org/ja/)に沿ってブログアプリを作る
- 女性がプログラミングに出会う機会を提供
- Tutorialを修了した後、作りたいアプリを作れるようになるには？

+++

### Tutorialとの差の体験：Where is settings.py?

```
.
├── accounts
├── blog
├── manage.py
├── mysite
│   ├── __init__.py
│   ├── settings
│   ├── urls.py
│   └── wsgi.py
├── static
└── templates
```

[本トークの開発用リポジトリ](https://github.com/ftnext/djangogirls-nextstep/tree/master/django)より

+++

### Django is Hot! But ...

- Djangoに注目：[Qiita2018年流行語大賞で3位](https://qiita.com/dcm_chida/items/15b9e7e835e3e5f9d5e5)
- Issue：注目されているDjangoには、入門者用チュートリアルを終えても、実務レベルとの間にギャップがある

+++

### おことわり：「実務レベル」

- 発表者は実務のWeb開発でDjangoを使った経験はありません
- 実務レベル=Djangoで作りたいアプリが作れる と想定
- 本発表を実務レベルに近づけるために、フィードバックは大歓迎です

+++

### ギャップを埋めるために

- Django Girls Tutorialのブログアプリを作り直す
- 実務でDjangoを使う上で必要と考える知見を共有
- Tutorialで扱っていないが、世のWebアプリで見かける機能について話します

+++

### Target Audience

- Django Girls Tutorialを最後までやってみた方
- Django Girls Tutorialと自分の作りたいアプリとの間にギャップを感じている方

Django Girls TutorialはDjangoのチュートリアルの一例として挙げています

+++

### Goal

- Django Girls Tutorialで扱っていない機能をDjangoで実現しようと思ったときに調べ方が浮かぶ
- GitHubにあるDjangoのコードを読んで参考にできる

+++

### Agenda

- Django Girls Tutorial クイックツアー（10min）
- ユーザまわりを実装（10min）
- この機能、どう作る？（10min）
- まとめ（5min）
- 質疑（5min）

+++

### トークのお供に

- [材料収集時にデプロイしたブログアプリ](https://ftnext.pythonanywhere.com/)
- [本トーク用ソースコード](https://github.com/ftnext/nextstep_djangogirls_tutorial)

手を動かしながら聞くのもいいと思います

---?include=django_congress_2019_blog_next_step/part1_quick_tour.md

---?include=django_congress_2019_blog_next_step/part2_user_management.md

---?include=django_congress_2019_blog_next_step/part3_features.md

### Agenda

- Django Girls Tutorial クイックツアー（10min）
- ユーザまわりを実装（10min）
- この機能、どう作る？（10min）
- **まとめ**（5min）
- 質疑（5min）

+++

### Django Girls Blogのネクストステップ

- ログイン機能まで：プロジェクト作成、名前空間、settings.py分割
- ユーザ管理を追加：ユーザ登録、パスワード再設定
- よく見かける機能：ページネーション、カスタムタグ／フィルタ、権限

+++

### 既存のソースコードを読むための知識

- プロジェクト作成、settings.py分割
- クラスベースビュー、ジェネリックビュー、認証ビュー

これらを知った今、見方がわかり、参考にできるはず

+++

### Djangoのコード例

- [PyCon Taiwanサイト](https://github.com/pycontw/pycon.tw)
- [cronote DRF勉強会](https://github.com/righ/djample)
- [MyMDB](https://github.com/tomaratyn/MyMDB)（後述の書籍のリポジトリ）

→ GitHubにあるDjangoのコードも参考にしましょう

+++

### 「この機能。どう実装する？」と思ったら

**二刀流** で調べましょう

- Google検索（検索エンジン）
- Djangoドキュメント内の検索（英語ドキュメントを検索）

+++

### ググる

- 「Django ページネーション」などでググる
- 見つかったブログ記事などを参考にしましょう
- 今回調べた範囲では、naritoさんや、okoppe8さん、thinkAmiさんの発信を優先して参考にしました（多謝）

+++

### 合わせてDjangoドキュメントで検索

- Django2.2系のブログ記事はまだ少ない
- 英語のDjangoドキュメント内を検索し、一次情報にあたって実装（読むときは日本語）
- ドキュメントで記述が少ない部分はソースコードを見る（認証ビューのところでソースを見ました）

+++

### 書籍情報

体系だった書籍で一緒に復習しましょう

- 『現場で使える Django の教科書』[基礎編](https://www.amazon.co.jp/dp/4802094744)・[実践編](https://www.amazon.co.jp/dp/B07L3DRGBT/)
- 『[基礎から学ぶ Django](https://www.amazon.co.jp/dp/486354247X/)』（期待を込めて）
- 『[Building Django 2.0 Web Application](https://www.amazon.co.jp/dp/B079DW6TRJ)』（参考にしましたが、説明不足気味です）

+++

### 最後に：実務レベルに至るには、情報をかき集めつつ手を動かそう

- 実務レベル = 作りたいアプリをDjangoで作れる状態
- GitHubで公開されたコード、Django強者のブログ、Djangoドキュメント・ソースコード、書籍
- 「手を動かすことは、エンジニアとしての自分の未来を創ること」（nikkie語録）

+++

### Special Thanks

- 登壇を応援してくださった勤務先のチームメンバー
- 登壇準備中は、京都アニメーションの『響け！ユーフォニアム』に支えていただきました
- そして、これまで教える機会を提供してくださった、Workshopやハンズオンの参加者の方々に

+++

### おまけ：デプロイについて

- ソースコードはPythonAnywhereで動作します
- ただし、[Freeプランでのメール送信](https://help.pythonanywhere.com/pages/SMTPForFreeUsers/)未設定のためパスワード再設定は動作しません
- 手順参考（暫定版）：https://ftnext.pythonanywhere.com/post/1/

+++

### ご清聴ありがとうございました

休憩時間やパーティーなどでフィードバックいただけると嬉しいです

Contact: [Twitter @ftnext](https://twitter.com/ftnext)／[匿名質問箱](https://peing.net/ja/ftnext)
