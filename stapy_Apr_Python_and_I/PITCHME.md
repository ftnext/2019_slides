## P(ython)&I
### 最初の落とし穴を避け、成功体験を積むために
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

- Pythonと私のこの1年とこれからの話
- Pythonを始めた時点（＝PythonのPの時点）が中心
- トークを通して、✨Pythonの魅力✨を伝えたい

+++

@snap[north]
### お前、誰よ / About nikkie
@snapend

@snap[west half-width-bullets]

@ul[](false)
- 平成2年生まれ
- 2016〜 ソフトウェアエンジニア
- Python歴1年（趣味でスタート、時々業務）
@ulend

@snapend

@snap[east half-width-bullets]

@ul[](false)
- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09〜 stapy 4代目LT王子
- アニメが好き
@ulend

@snapend

@snap[south span-100]
注: 今回の登壇で示す見解は、nikkie個人の見解です(所属組織とは無関係です)
@snapend

+++

@snap[west snap-seventy-percent-image]
![CoLabユーザーが技術書を書いてみた](stapy_Apr_Python_and_I/assets/colab_book6_cover.png)
@snapend

@snap[east half-width-bullets]

### 告知：技術書典6で合同誌参加

@ul[](false)
- 2019/04/14(日)＠池袋 [サポーターズCoLab く17](https://techbookfest.org/event/tbf06/circle/36070001)
- 2019年1月,3月のKaggleタイタニックコンペハンズオンを記事化
- ソースコードは[公開](https://www.kaggle.com/ftnext/spzcolab-techbook6)しています
@ulend

@snapend

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

### なぜPythonを始めたか

- 「悔しくって死にそう」：業務で力不足を痛感😢
- 2017年3月（1年目）、進めていたプロジェクト(PHP)で大遅延
- 「**独力で何か作れるようになりたい**」と強く思った

+++

### 趣味で始めたPython

- 2017年11月頃スタート
- 2017年1月にPyNyumon（スクレイピングハンズオン）
- スタートするまでに数回使ったが、つまづかなかったので印象がよかった

+++

@snap[north-west snap-north-west-image]
![退屈なことはPythonにやらせよう 表紙](stapy_Apr_Python_and_I/assets/taipy_book_cover.jpeg)
@snapend

@snap[east half-width-bullets]
### [退Py](https://www.oreilly.co.jp/books/9784873117782/)を手に取る

@box[span-100](<a href="http://automatetheboringstuff.com/chapter17/" rel="noopener noreferrer" target="_blank">17章</a> Pillowによる画像処理)

@ul[](false)
- 拡大、縮小
- 画像を並べて配置
@ulend

@snapend

@snap[south-west snap-south-west-image]
![退Py17章 画像処理の例](stapy_Apr_Python_and_I/assets/taipy_ch17_6.jpg)
@snapend

+++

### 退Pyで画像処理の事例を見て

- Pythonって画像扱えるんだ！🤩
- モザイクアート作ってみようかな
- モザイクアート＝画像を寄せ集めて、別の絵を浮かび上がらせる

+++?image=stapy_Apr_Python_and_I/assets/python_and_i__mosaic_art.jpg&size=cover

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
  - python.orgからダウンロード & venv（後述）
- Pythonを教え始めて：「始めの成功体験、私が思っているよりハードル高い？」🤔

+++

@snap[north]
### Pythonのインストール方法
@snapend

@snap[west]
@box[span-100 bg-blue text-white rounded](python.orgからダウンロード)

@ul[](false)
- [Windows向け手順](https://www.python.jp/install/windows/index.html)
- [macOS向け手順](https://www.python.jp/install/macos/index.html)
@ulend

@snapend

@snap[east]
@box[span-100 bg-blue text-white rounded](Anaconda)
@box[span-100](<a href="https://www.python.jp/install/anaconda/index.html" rel="noopener noreferrer" target="_blank">Anaconda導入手順</a>)
@snapend

@snap[south]
注：[python.jpの環境構築ガイド](https://www.python.jp/install/install.html)をもとにしています
@snapend

Note:

Pythonのインストール方法について人数を聞く

+++

### Anacondaとは

- Python + データサイエンスで使うパッケージ(例: `numpy`, `scikit-learn`)
- パッケージ：第三者が書いたPythonのコード（インストールしたパッケージを`import`して、関数やクラスを使う）
- Anacondaで使うほうが性能がいいパッケージもある（`tensorflow`）

+++

### 環境構築の落とし穴

- Pythonを始めた直後につまづく方に見られるケース：
  - python.orgからダウンロード && Anacondaも利用
- Pythonを **重複してインストール** している

+++?color=#333333

### @css[text-white](Pythonのインストールはどれか1つだけにしよう)

@ul[list-bg-black](false)

- 記事の通りにやる姿勢は素晴らしい👏
- Pythonのインストール方法が自分とは異なる記事を参照するときは、記事を読み替えよう

@ulend

+++

### 例：機械学習やりたい

- あなたはpython.orgからPythonを入れた
- Anacondaを使って機械学習を解説する記事を見つけた

Q: どうしますか？

+++

### A: Anacondaを入れる

# @css[fragment](🙅)

+++

### 想定解：必要なパッケージを`pip install`

- Anacondaに最初から入っているパッケージ（`numpy`, `scikit-learn`など）が手元の環境にはない
- Anacondaを入れるのではなく、**個々のパッケージだけを** インストール
- 別解：python.orgからPythonを入れて機械学習をする記事を探す

+++

### 別の事例

- あなたはAnacondaでPythonをインストールした
- 参考記事はpython.orgからダウンロードして環境構築している
- その記事の中でパッケージを`pip install`している

Q: どうしますか？

+++

### A: Anaconda環境でも`pip install`する

# @css[fragment](🙅)

+++

### Anacondaを使うなら：pipはcondaに読み替えよう

- `pip`と`conda`もパッケージを管理するためのコマンド
- **どちらかに絞って使う** ことをオススメします
- AnacondaでPythonをインストールしているならば、パッケージは`conda install`で入れましょう

+++

### pipはcondaに読み替えよう 参考

>慣れるまでは、できるだけ Condaだけを使ってパッケージをインストールするようにしましょう。

[python.jp Condaコマンド](https://www.python.jp/install/anaconda/conda.html) より

+++

### ネクストステップ：仮想環境

- 開発ごとに隔離された環境のこと
- 同じパッケージの **バージョン違い** を1台のPCに **共存** させられるのでオススメ

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
- 質問は答える方の学びにもなるので、遠慮は不要
- ここまで聞いた皆さんなら答えられる or この資料を案内

+++

### 「質問タイムです」（sli.do 確認）

今回は環境構築を中心に扱いたいので、残りは時間と相談して進めます🙇‍

---

### 目次：P(ython)&I

- nikkie "オリジン"：最初の成功体験
- オリジンを支えた環境構築
- **私とPython（事例紹介）**

+++

### 私とPython（事例紹介）

- これまでの1年でPythonに夢中になった事例(2点)
- 「作れるようになりたい」を実現するためのこれからの取り組み(2点)

+++

### これまで-1：「もしその瞬間が来たら、それがお前がPythonにハマる瞬間だ」

- 開発を続ける中で、その瞬間は突然やってきた
- Pythonの出す **エラーが読める** ようになった
- 毎回エラー文をググらなくても開発できる

+++

### 例：エラーが読める

- Python🐍「NameError（＝ctiyなんてないですよ）」
- →私「あっ、変数名のタイポだ」

```python
>>> city = "Tokyo"
>>> ctiy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'ctiy' is not defined
```

コードは[Django Girls Tutorialより](https://tutorial.djangogirls.org/ja/python_introduction/)

+++

### これまで-2：stapyをきっかけにPythonの広い世界へ漕ぎ出す

- stapyで聞く **幅広いトーク**（Web、機械学習、etc.etc.）
- トークをきっかけに触った内容を懇親会でアウトプット
  - LTへのフィードバック、誠にありがとうございます🙇‍

+++

### stapyのLT駆動学習のすゝめ

- [nao_yさん提唱](https://gitpitch.com/NaoY-2501/GitPitch-Slides?p=stapy31_20180110#/6/2)「懇親会のLTを目指して学習をする」
- 思うに、**アウトプットの敷居は低くていい**
	- 「このパッケージのチュートリアルをやりました。ここがポイントでした💡」
	- 「このパッケージのここがわかりません。助けてください🙏」

+++

### これから-1 [DjangoCongress JP](https://djangocongress.jp/)話します

- Djangoに入門した後、**アプリを作れるようになるための情報が少ない** ように感じる
- →Django Girls Tutorialのブログアプリを作り直して知見をアウトプット

+++

### 皆さんと一緒に作り上げるトークに

- Djangoに入門してわからないことがある方は、「ここが知りたい」という声をお寄せください
- Djangoに詳しい方、レビュワーとして募集中です

+++

### これから-2 stapy 長野 に参加して

- 2019/03 [stapy in 長野](https://startpython.connpass.com/event/119465/)「社内WebシステムのPython活用秘話」
- 日本システム技研さんのDjango力は、**業務改善かつ修行としてのDjango開発** で培われた
- 例：Excelの勤怠管理システムをDjangoアプリでリプレース

+++

### 個人開発で未来を作る💪（build future）

- 手を動かさなければ身につかないと感じていた
- stapy長野での気づき：「自分が **アプリを作る** ことで、知識が身につき、**自分の未来も創ることにつながる**」

---

### まとめ：P(ython)&I

- Pythonと私のこれまでとこれからを共有してきた
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

- Pythonのインストール方法が自分と違う記事は **読み替え** よう
- 環境構築でつまづきそうだったら、**人に聞こう**（一つの質問先として[@ftnext](https://twitter.com/ftnext)）
- 環境構築を乗り越えて最初の成功を体験したら、stapyでLTしませんか？

+++

### おまけ：Pythonの知り合いを増やす

- コミュニティで知り合いを増やすと、わからないことも質問できる
- PyCon JP スタッフ募集中です！
- [PyCon JP 2019 スタッフ募集およびNOCチームスタッフ募集開始](https://pyconjp.blogspot.com/2019/03/pycon-jp-2019-staff-noc.html)

+++

### ご清聴ありがとうございました
### 🤞Let's build future!🤞
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
