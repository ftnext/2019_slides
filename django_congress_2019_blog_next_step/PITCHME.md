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
- 2018/05~ Django Girls Tutorial 翻訳、Workshopコーチ
- Django Girls Tutorialをベースにしたハンズオン開催 [2019/01](https://gitpitch.com/ftnext/2019_slides/master?p=elv_Jan_django_errorfriends/), [2019/02](https://gitpitch.com/ftnext/2019_slides/master?p=elv_Feb_django_developcompass/)

+++

### アンケート

1. Django Girls Tutorialに取り組んだことのある方🙋‍
2. 実務や個人開発でDjangoを使っている方🙋‍

+++

### 問題意識：There is a gap

Django Girls Tutorial修了 ≠ 実務でDjangoが使える

Tutorialを終えても、作りたいアプリが作れるわけではない

+++

### ギャップの例：Where is settings.py?

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

### ギャップを埋めるために

- Django Girls Tutorialのブログアプリを作り直す
- 実務でDjangoを使う上で必要と考える知見を共有

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

### おことわり

- タイトルで「実務レベル」としていますが、発表者は実務のWeb開発でDjangoを使った経験はありません
- 実務レベル=Djangoで作りたいアプリが作れる と想定
- 本発表を実務レベルに近づけるために、フィードバックは大歓迎です

+++

### Agenda

- Django Girls Tutorial クイックツアー（10min）
- ユーザまわりを実装（10min）
- この機能、どう作る？（10min）
- まとめ（5min）
- 質疑（5min）

---?include=django_congress_2019_blog_next_step/part1_quick_tour.md

---?include=django_congress_2019_blog_next_step/part2_user_management.md

---?include=django_congress_2019_blog_next_step/part3_features.md
