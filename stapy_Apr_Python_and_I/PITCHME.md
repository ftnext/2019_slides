## P(ython)&I
### Python最初の成功体験と最初の落とし穴の回避策
#### みんなのPython勉強会#44 (2019/04/10) nikkie

---

### 🌸4月、始まりの季節🌸

- プログラミングに興味があり、Pythonを始める方
- 別の言語からPythonを始める方

そんな方にこのトークを送ります

Note:

Pythonで別の領域に渡る方（例：Web→機械学習）にも環境構築の話が参考になれば幸いです

+++

### 概要：P(ython)&I

- Pythonと私のこの1年とこれから
- Pythonを始めた時点（PythonのPの時点）についての経験を共有
- トークを通して、✨Pythonの魅力✨を伝えたい

+++

### お前、誰よ / About nikkie

@snap[west]

@ul
- 平成2年生まれ
- 2016〜 ソフトウェアエンジニア
- Python歴1年（趣味でスタート、時々業務）
@ulend

@snapend

@snap[east]

@ul
- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09〜 stapy 4代目LT王子
- アニメが好き
@ulend

@snapend

+++?image=stapy_Apr_Python_and_I/assets/colab_book6_cover.png&size=contain&opacity=50

### 最近のアウトプット：技術書典6 く17

- 2019/04/14(日) 池袋にて開催
- 合同誌に参加: [サポーターズCoLab く17](https://techbookfest.org/event/tbf06/circle/36070001)
- 2019年1月,3月のKaggleタイタニックコンペハンズオンを記事化
- ソースコードは[公開](https://www.kaggle.com/ftnext/spzcolab-techbook6)しています

+++

### 目次：P(ython)&I

- nikkie "オリジン"：最初の成功体験
- オリジンを支えた環境構築
- 私とPython（事例紹介）

---

### 目次：P(ython)&I

- **nikkie "オリジン"：最初の成功体験**
- オリジンを支えた環境構築
- 私とPython（事例紹介）

+++

### nikkie "オリジン"

Pythonを始めたあとの最初の成功体験を共有

- Pythonを始めたきっかけ
- 最初に作ったもの：モザイクアート

+++

### 「悔しくって死にそう」

- なぜPythonを始めたか：業務で力不足を痛感して😢
- 2017年3月（1年目）、進めていたプロジェクト(PHP)で大遅延
- 「独力で何か作れるようになりたい」と強く思った

+++

### 趣味で始めたPython

- 2017年11月頃スタート
- 2017年1月にPyNyumon（スクレイピングハンズオン）
- スタートするまでに数回使い、つまづくことはなかった

+++

### "自動化事例集"<br>『[退屈なことはPythonにやらせよう](https://www.oreilly.co.jp/books/9784873117782/)』

![退屈なことはPythonにやらせよう 表紙](stapy_Apr_Python_and_I/assets/taipy_book_cover.jpeg)

+++

### 退Py[17章](http://automatetheboringstuff.com/chapter17/) 画像処理

Pillowというパッケージで画像処理（切り取り、配置、拡大、縮小など）

![退Py17章 画像処理の例](stapy_Apr_Python_and_I/assets/taipy_ch17_6.jpg)

+++

### 退Pyで画像処理の事例を見て

- Pythonって画像扱えるんだ！🤩
- モザイクアート作ってみようかな

+++?image=stapy_Apr_Python_and_I/assets/python_and_i__mosaic_art.png&size=cover

Note:

2017年12月

+++

### 私とPython、最初の成功体験

- 「作ってみようかな」を実現できた😆
- ほぼ英文（例：`if not`）なのはポイント高い
- インデントは最初はとっつきにくかったが、慣れた

---

### 目次：P(ython)&I

- nikkie "オリジン"：最初の成功体験
- **オリジンを支えた環境構築**
- 私とPython（事例紹介）

+++

### 成功体験を支えた環境構築

- 私「Pythonでは、"作ってみたい"を実現するハードルはそんなに高くない」😆
- Pythonを教え始めて：「始めの成功体験、私が思っているよりハードル高い？」🤔

+++

### Pythonのインストール方法

- [python.org](https://www.python.org/)からダウンロード [Windows](https://www.python.jp/install/windows/index.html) [macOS](https://www.python.jp/install/macos/index.html)
- [Anaconda](https://www.python.jp/install/anaconda/index.html)
- etc

注：[python.jpの環境構築ガイド](https://www.python.jp/install/install.html)をもとにしています

Note:

Pythonのインストール方法について人数を聞く

+++

### Anacondaとは

- Python + データサイエンスで使うパッケージ(例: `numpy`, `scikit-learn`)
- パッケージ：第三者が書いたPythonのコード（`import`して関数やクラスを使う）
- パッケージによっては、Anacondaで使うほうが性能がいいことがある

+++

### 環境構築の落とし穴

- 成功体験でつまづく方に見られるケース：
  - python.orgからダウンロード && Anacondaも利用
- Pythonを **重複してインストール** している

+++

### インストールはどれか1つだけにしよう。
### 自分の環境とインストールの仕方が異なる記事を参照するときは、インストールの部分を読み替えよう

記事の通りにやる姿勢は素晴らしいです。ただし一部読み替えが必要です

+++

### 例：機械学習やりたい

- あなたはpython.orgからPythonを入れた
- Anacondaを使って機械学習を解説する記事を見つけた

Q: どうしますか？

+++

### A: Anacondaを入れる

@css[fragment](# 🙅)

+++

### 想定解：必要なパッケージを`pip install`

- 現状と解説記事の違い：Anacondaに最初から入っているパッケージ（`numpy`, `scikit-learn`など）が手元にはない
- 別解：python.orgからPythonを入れて機械学習をする記事を探す

+++

### 逆の事例

- あなたはAnacondaでPythonをインストールした
- python.orgからダウンロードして機械学習を解説する記事を見つけた（`pip install`している）

Q: どうしますか？

+++

### A: Anaconda環境でも`pip install`する

@css[fragment](# 🙅)

+++

### Anacondaを使うなら：pipはcondaに読み替えよう

- AnacondaでPythonをインストールしているならば、パッケージは`conda`で入れましょう
- 見つけた情報の`pip install`は全て`conda install`に読み替えましょう

+++

### pipはcondaに読み替えよう 参考

>慣れるまでは、できるだけ Condaだけを使ってパッケージをインストールするようにしましょう。

[python.jp Condaコマンド](https://www.python.jp/install/anaconda/conda.html) より

+++

### ネクストステップ：仮想環境

- プロジェクトごとに隔離された環境のこと
- 同じパッケージのバージョン違いを1台のPCに共存させられるのでオススメ

+++

### python.orgからダウンロードした場合の仮想環境

- 1つの方法として`venv`モジュールを使う
- 例：`python3 -m venv env` (macOS想定)
- 詳しくは[PyNyumonテキスト](https://github.com/pynyumon/pynyumon/blob/master/1_python_basics.md)

+++

### Anacondaで仮想環境を使う

- `conda`コマンドで作成できる
  - 作成：`conda create`
  - 切り替え：`conda activate`
- 参考：[python.jp Condaコマンド](https://www.python.jp/install/anaconda/conda.html)

+++

### 「私(たち)は、頼ってほしいよ」

- 環境構築でつまづいたら人に聞こう（懇親会やもくもく会）
- やりたいことに取り組む前の環境構築でつまづいて諦めるのはもったいない
- 質問は答える方の学びにもなるので、遠慮は不要

---

### 目次：P(ython)&I

- nikkie "オリジン"：最初の成功体験
- オリジンを支えた環境構築
- **私とPython（事例紹介）**

+++

### 私とPython（事例紹介）

- これまでの1年とこれからを簡単に共有
- Pythonに夢中になった事例(2点)
- 「作れるようになりたい」を実現するための取り組み(2点)

+++

### これまで-1：「それが、お前がPythonにハマる瞬間だ」

- 開発を続ける中で、それは突然やってきた
- Pythonの出す **エラーが読める** ようになった
- 毎回エラー文をググらなくても開発できる＝Pythonが道具になった

+++

### 例：エラーが読める

Python🐍「ctiyなんてないですよ」→私「あっ、変数名のタイポだ」

```python
>>> city = "Tokyo"
>>> ctiy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'ctiy' is not defined
```

コードは https://tutorial.djangogirls.org/ja/python_introduction/ より

+++

### これまで-2：Pythonの広い世界へ漕ぎ出す

1つの言語で幅広い領域を扱える

- 自動化スクリプト
- Web
- 機械学習
- 組み込み
- etc

+++

### 漕ぎ出す一助に、stapyのLT駆動学習

- 懇親会のLTを目指して学習をする([nao_yさん提唱](https://gitpitch.com/NaoY-2501/GitPitch-Slides?p=stapy31_20180110#/6/2))
- アウトプットの敷居は低くていい
	- 「このパッケージのチュートリアルをやりました」
	- 「このパッケージのここがわかりません」

+++

### LTへのフィードバック、誠にありがとうございます🙇‍

- 私のLT駆動学習
  - [2018](https://github.com/ftnext/2018_LTslides) Djangoにモザイクアートなど
  - [2019](https://github.com/ftnext/2019_slides) pandasの基礎を確認して共有など
- 不完全なプログラムでもアウトプットすることでフィードバックをいただける

+++

### これから-1 [DjangoCongress JP](https://djangocongress.jp/)話します

- Django Girls TutorialはDjangoに入門するのに最適
- しかし、それだけでは、アプリを作れるようにならないのでは？
- →Tutorialで扱うブログを作り直して知見をアウトプット

+++

### 皆さんと一緒に作り上げるトークに

- Djangoに入門してわからないことがある方はお知らせください
- 「ここが知りたい」という声に応じてトークの内容を変えます
- Djangoに詳しい方、レビュワーとして募集中です

+++

### 2. stapy 長野 に参加して

- 2019/03 [stapy in 長野](https://startpython.connpass.com/event/119465/)「社内WebシステムのPython活用秘話」
- **業務改善かつ修行としてのDjango開発**
- →日本システム技研さんはDjango力を培った

+++

### 2. 個人開発で未来を作る💪（build future）

- 「作らなければ身につかない」
- 「自分が **アプリを作る** ことで、知識が身につき、**自分の未来も創ることにつながる**」
- （アプリ開発に限らず、手を動かすことは未来につながると考えています）

---

## まとめ：P(ython)&I

- Pythonと私のこの1年を共有してきた
- まとめ1：Pythonの魅力
- まとめ2：Pythonを始めたときにつまづかないために

+++

### Pythonの魅力

- ほぼ英文のコード
- 広い領域を1つの言語で扱える
- 慣れると美しいインデント
- 私にとっては、エラーが読める言語

+++

### Pythonを始めたときにつまづかないために

- Pythonのインストール方法が自分と違う記事は読み替えよう
- 環境構築でつまづきそうだったら、人に聞こう（一つの質問先として[@ftnext](https://twitter.com/ftnext)）
- +α：広い世界へ漕ぎ出す一助にアウトプット（stapyでLT駆動学習）

+++

### おまけ：Pythonの知り合いを増やす

- コミュニティで知り合いを増やすと、わからないことも質問できる
- PyCon JP スタッフ募集中です！
- [PyCon JP 2019 スタッフ募集およびNOCチームスタッフ募集開始](https://pyconjp.blogspot.com/2019/03/pycon-jp-2019-staff-noc.html)

+++

### ご清聴ありがとうございました
### 🤞Let's build future!🤞
