## 【羅針盤を手に入れる】
# Django基礎<br>ハンズオンⅡ
#### eLV勉強会 2019/02/14 nikkie

+++

## Welcome to
## Django基礎ハンズオンⅡ

+++

### アンケート🙋 1/2

- 前回来られた方
- 今回初めての方

+++

### アンケート🙋 2/2

Web開発経験について（このハンズオンを除いて）
‍
- Djangoの経験あり
- 他の言語で経験あり(PHP, Rails)
- はじめて

+++

### 自己紹介（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 3年目のソフトウェアエンジニア（Web開発、機械学習）
- 2018〜 Django Girls Tutorial翻訳に参加、Workshopコーチ

+++

### TA：nao_yさん

- [@NaoY_py](https://twitter.com/NaoY_py)
- みんなのPython勉強会 運営メンバーのお一人

---

## 羅針盤？

+++

### 前回：エラーは友達

- Djangoと仲良くなろうとするとエラーが立ちはだかる
- 前回はエラーの対処の仕方を学び、エラーと友達になった

+++

![Djangoと仲良くなろうとするとエラーが立ちはだかる](elv_Jan_django_errorfriends/assets/django_taik_images.002.png)

+++

![エラーの対処の仕方を学び、エラーと友達になった](elv_Jan_django_errorfriends/assets/django_taik_images.004.png)

+++

### エラーと友達になったあと

- Djangoと友達になる（使いこなす）段階
- Djangoは機能が豊富
- それゆえに把握しきれない🤨

+++

![DjangoにはURL・モデル・ビュー・テンプレートなどなど用意されている](elv_Feb_django_developcompass/assets/django_talk_image.001.png)

+++

![作りたい機能（例：ブログ記事の詳細ページ）を実現するにはまず何をいじればいい？](elv_Feb_django_developcompass/assets/django_talk_image.002.png)

+++

## そこで、今回<br>羅針盤（開発手順）を<br>手に入れます

---

### ハンズオンを通して

- 一緒に手を動かしながら@color[#ff9400](Djangoの開発手順)を学んでいく
- ハンズオンの後は、Djangoの開発手順（＝羅針盤）がわかった状態
- 前回学んだ「このエラーにはこうする」と合わせて、Djangoを使って作りたいものが作れる（に近づく）

+++

### ハンズオンの題材

- @color[#ff9400](ブログアプリ)に機能追加していく
- ハンズオンの一部は[Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)に基づく

+++

### ブログアプリ機能追加手順

0. ブログアプリの機能のおさらい
1. ブログ画面からブログ記事を作る
2. ブログ記事の詳細が見られるようにする
3. ブログ記事に画像を追加できるようにする

+++

### ブログ画面からブログ記事を作る

![](elv_Jan_django_errorfriends/assets/part3/4_post_from_form.png)

+++

### ブログ記事の詳細が見られるようにする

![](elv_Feb_django_developcompass/assets/part2/4_display_detail.png)

+++

### ブログ記事に画像を追加できるようにする

<span class="sixty-percent-img">
![](elv_Feb_django_developcompass/assets/part3/5_post_detail_with_image.png)
</span>

---

### 注意事項

- 内容を絞ってDjango Girls Tutorialを進めます
  - スライドのソースコードをコピペしながら進めます
- 解説はDjangoに絞っています
	- Pythonの基礎、HTML、CSSについては詳しく取り上げません
- お手元のPCの中だけで動かします（今回はデプロイを扱いません）

+++

### 実りあるハンズオンにするために🙇

- ハンズオン中、質問は随時受け付けます（うまくいかないときはお知らせください）
- 隣近所で教え合っていただけると助かります（わからなければ遠慮なくサポートを呼んでください）

+++

### ハンズオンを始める前に

1. コマンドライン（コマンドプロンプトやターミナル）を起動
2. `cd errorfriends`（errorfriendsディレクトリに移動）
3. Django開発用環境を有効化（次のスライド）

+++

### 手順3 開発用環境の有効化

- Django開発用環境をmyvenvとしています（[環境構築参考記事](https://qiita.com/ftnext/items/082ec8fe96f26b181fc5)）
- 仮想環境を使う方
  - Windows: `myvenv\Scripts\activate`
  - macOS: `source myvenv/bin/activate`
- Anacondaの方： `activate myvenv`

+++

### 【羅針盤を手に入れる】<br>Django基礎ハンズオンⅡ

0. ブログアプリの機能のおさらい（20分）
1. ブログ画面からブログ記事を作る（35分）
2. ブログ記事の詳細が見られるようにする（25分）
3. ブログ記事に画像を追加できるようにする（35分）

---?include=elv_Feb_django_developcompass/part0.md

---?include=elv_Feb_django_developcompass/part1.md

---?include=elv_Feb_django_developcompass/part2.md

---?include=elv_Feb_django_developcompass/part3.md

---

### まとめ

- ハンズオンでやったことの振り返り
- 羅針盤について
- ハンズオン後のDjangoの学び方案

+++

### 【羅針盤を手に入れる】Django基礎ハンズオンⅡ

0. ブログアプリの機能のおさらい（20分）
1. ブログ画面からブログ記事を作る（35分）
2. ブログ記事の詳細が見られるようにする（25分）
3. ブログ記事に画像を追加できるようにする（35分）

+++

### 羅針盤

<span class="eighty-percent-img">
![](elv_Feb_django_developcompass/assets/django_compass.png)
</span>

+++

### ブログアプリのハンズオン

- 目的地はブログアプリ
- エラーと友達になった
- 羅針盤を手に入れた

+++

### 次の目的地はあなたが決める

- 手には羅針盤
- 旅の仲間はエラー
- あなたが決めた目的地へDjangoという船で向かってください

+++

### ハンズオン後のDjangoの学び方案

- [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)で復習（デプロイはスキップしてよい）
- [Django 投票アプリ チュートリアル](https://docs.djangoproject.com/ja/2.1/intro/tutorial01/)
- 参考：akiyokoさん [初学者・初級者向け Django の学習ロードマップ](https://akiyoko.hatenablog.jp/entry/2018/12/01/133427)

+++

![羅針盤を手に、エラーを仲間に、あなたが決めた目的地へDjangoという船で向かってください](elv_Feb_django_developcompass/assets/django_talk_image.003.png)

+++

### 参考文献

- [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)
- Qiita [@okoppe8 [Django] ファイルアップロード機能の使い方 [基本設定編]](https://qiita.com/okoppe8/items/86776b8df566a4513e96)
- [『プロになるためのWeb技術入門』](https://www.amazon.co.jp/dp/4774142352)

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！

Contact: [Twitter @ftnext](https://twitter.com/ftnext)

+++

### EOF
