## P(ython)&I
### Pythonの魅力、そして最初の落とし穴を回避する（仮）
#### みんなのPython勉強会#44 (2019/04/10) nikkie

---

### 4月、始まりの季節

- Pythonでプログラミングを始める方
- 別の言語からPythonを始める方
- Pythonで別の領域に渡る方（例：Web→機械学習）

そんな方にこのトークを送ります

+++

### 概要：P(ython)&I

- Pythonと私のこの1年とこれから
- Pythonの魅力を伝えたい
- Pythonを始めるにあたってつまづかないように情報提供したい

+++

### 自己紹介

- 平成2年生まれ。Pythonは趣味がメイン、時々業務
- 4年目のソフトウェアエンジニア
- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09〜 stapy 4代目LT王子
- アニメが好き

+++

### 今週末は技術書典♪

- 合同誌に参加しました！：[サポーターズCoLab く17](https://techbookfest.org/event/tbf06/circle/36070001)
- 2019年1月,3月のKaggleタイタニックコンペハンズオンに **交差検証**、**グリッドサーチ** を追加して記事化
- ソースコードは[公開](https://www.kaggle.com/ftnext/spzcolab-techbook6)しています

---

### 目次：P(ython)&I

- nikkie "オリジン"：モザイクアートという成功体験
- 成功体験を支えた環境構築
- Pythonにハマる：「エラーが読める！」
- 広い世界に漕ぎ出す

+++

### 目次：P(ython)&I

- **nikkie "オリジン"：モザイクアートという成功体験**
- 成功体験を支えた環境構築
- Pythonにハマる：「エラーが読める！」
- 広い世界に漕ぎ出す

+++

### nikkie "オリジン"

- 「悔しくって死にそう」→なにか作れるように→Python
- 2017年12月モザイクアートをPythonで作る
- 2017年1月にPyNyumonしていた（スクレイピングハンズオン）

+++

### 「悔しくって死にそう」

- 2017年3月（1年目）、進めていたプロジェクトで大遅延
- 力不足を痛感。何か作れるようになりたい→趣味としてPython
- 2017年1月にPyNyumonしていた（スクレイピングハンズオン）

+++

### 作ってみる：モザイクアート

- Pythonによる自動化の事例集『[退屈なことはPythonにやらせよう](https://www.oreilly.co.jp/books/9784873117782/)』
- [17章](http://automatetheboringstuff.com/chapter17/) Pillowというパッケージで画像処理（拡大、縮小など）
- スライド：[Pillowでモザイクアート](https://speakerdeck.com/ftnext/pillow-mosaic-art-nyumon)

+++

### こんなの作りました

TODO：モザイクアートを出す

+++

### Pythonを始めてみて

- 気に入った点：ほぼ英文（例：`if not`）
- インデントは最初はとっつきにくかったが、慣れた
- venvによる仮想環境を知っていたからつまづかなかった（次で話します）

---

### 目次：P(ython)&I

- nikkie "オリジン"：モザイクアートという成功体験
- **成功体験を支えた環境構築**
- Pythonにハマる：「エラーが読める！」
- 広い世界に漕ぎ出す

+++

### 成功体験を支えた環境構築

- 始めの成功体験、私が思っているより難しい？
- Pythonの共存が多い（例：python.orgからダウンロード & Anaconda）
- 原因は情報氾濫？（python.orgから入れた記事、Anacondaで入れた記事が混在）
- 注：venvとconda以外は今回は扱いません

+++

### Pythonのインストールはどれか1つだけにしよう

- python.orgからPythonをインストールしたら、Anacondaは使わない
- Anacondaを使うなら、python.orgからPythonをインストールしない
- パッケージのインストール方法を読み替えよう

+++

### python.org派：pip & venv

- パッケージは`pip`で入れる
- プロジェクトごとに隔離された環境（仮想環境）を作るのをオススメ（同じパッケージのバージョン違いを共存させられる）
- `python3 -m venv env`
- 詳しくは[PyNyumonテキスト](https://github.com/pynyumon/pynyumon/blob/master/1_python_basics.md)

+++

### Anaconda派：pipはcondaに読み替えよう

- パッケージは`conda`で入れる
- 見つけた情報の`pip install`は全て`conda install`に読み替えましょう
- 参考：[python.jp Condaコマンド](https://www.python.jp/install/anaconda/conda.html)

>慣れるまでは、できるだけ Condaだけを使ってパッケージをインストールするようにしましょう。

+++

### 「私は、頼ってほしいよ」

- 環境構築でつまづいたら人に聞こう（懇親会やもくもく会）
- やりたいことに取り組む前の環境構築でつまづいて諦めるのはもったいない
- 質問は答える方の学びにもなるので、遠慮は不要

---

### 目次：P(ython)&I

- nikkie "オリジン"：モザイクアートという成功体験
- 成功体験を支えた環境構築
- Pythonにハマる：「エラーが読める！」
- 広い世界に漕ぎ出す

+++

### 「それが、お前がPythonにハマる瞬間だ」

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

### エラーが読める

- エラーメッセージを通してPythonと会話しながら開発している状態
- 至るには、エラーとその解決を数多く経験
- ショートカットに『[スラスラ読める Pythonふりがなプログラミング](https://book.impress.co.jp/books/1117101140)』？

---

### 目次：P(ython)&I

- nikkie "オリジン"：モザイクアートという成功体験
- 成功体験を支えた環境構築
- Pythonにハマる：「エラーが読める！」
- **広い世界に漕ぎ出す**

+++

### 広い世界に漕ぎ出す

私の場合は、業務やアウトプットドリブンで

- Web開発（Django、Flask）
- 機械学習
- エクセル自動化（openpyxl）

+++

### Pythonの魅力：広い領域を扱える

- 自動化スクリプト
- Web
- 機械学習
- 組み込み

+++

### 漕ぎ出す一助に、stapyのLT駆動開発

- アウトプットの敷居は低くていい
	- 「このパッケージのチュートリアルをやりました」
	- 「このパッケージのここがわかりません」
- 不完全なプログラムでもアウトプットすることでフィードバックをいただける（多謝）

+++

### LT駆動開発の例

- 2018年4月 [Djangoにモザイクアート](https://gitpitch.com/ftnext/2018_LTSlides/master?p=stapy_April_django#/)
- Django Girls Tutorialを参考に、モザイクアートを作る簡単なアプリケーションを作った

+++

TODO：バージョンアップしたモザイクアート×Django（GCPで動かしたい）

+++

## まとめ：P(ython)&I

- Pythonと私のこの1年を共有してきた
- まとめ1：Pythonの魅力
- まとめ2：Pythonを始めたときにつまづかないための情報提供

+++

### Pythonの魅力

- ほぼ英文のコード
- 読みやすいエラー
- 広い領域を1つの言語で扱える

+++

### Pythonを始めてつまづかないために

- 環境構築の方法は1つに決めて読み替えよう（python.orgかAnacondaかそれ以外か）
- 環境構築でつまづきそうだったら、人に聞こう（一つの質問先として[@ftnext](https://twitter.com/ftnext)）
- +α：広い世界へ漕ぎ出す一助にアウトプット（LT駆動開発）

---

### nikkie "ライジング"

- これまでを振り返ったあとは、**これから** の話
- 「作れる」エンジニアへの憧れ、皆さんと同じだと思っています
- 「作れる」に近づくために2点共有

+++

### 1. DjangoCongress JP話します

- Django Girls TutorialはDjangoに入門するのに最適
- 実務で扱うDjangoアプリとの間にはギャップあり（Django Girls Tutorialだけで作れるようにならない）
- Tutorialで扱うブログを作り直して知見をアウトプット

+++

TODO：Django Girlsのブログ、アップデートしてこうなっています

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

### 2. 個人開発で未来を作る（build future）

- 「作らなければ身につかない」（この3年業務でメインに書いてきたのは日本語。業務で書けないから余暇でコードを書いてきた）
- 「自分が **アプリを作る** ことで、知識が身につき、**自分の未来も創ることにつながる**」

+++

### ご清聴ありがとうございました
### Let's build future!
