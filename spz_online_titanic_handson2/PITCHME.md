## Kaggleタイタニックハンズオン
#### エンジニア学生向けオンライン勉強会
#### 2019/04/12 nikkie

---

### アイスブレイク

YouTubeのコメントに勉強会に参加したきっかけを投稿してみてください😁

例「興味のあったKaggleを体験してみたいです」

+++

### お前、誰よ

- ハンドルネーム nikkie, Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2019年[1月](https://supporterzcolab.com/event/677/)・[3月](https://supporterzcolab.com/event/740/)サポーターズでKaggleハンズオン登壇
- エンジニア4年目（業務でPython書き始めました）。アニメが好き（アイマス、ユーフォ）

+++

### サポーターズCoLabにて、タイタニック関連のアウトプット

- [1月ハンズオン資料](https://gitpitch.com/ftnext/2019_slides/master?p=spz_Jan_titanic_handson/)
- [3月ハンズオン資料](https://gitpitch.com/ftnext/2019_slides/master?p=spz_Mar_titanic_handson2/)
- [技術書典6 合同誌](https://techbookfest.org/event/tbf06/circle/36070001)

+++

### Kaggleのアカウント作成

**事前に作っていない人** は作成をお願いします🙇

まず https://www.kaggle.com/account/login にアクセス

+++

![お好みの登録方法で進めてください（FB, Google, Yahoo, Email）](spz_Jan_titanic_handson/assets/kaggle_register.png)

+++

### （参考）SMS認証

- 国コード +81 80-XXXX-XXXX（国コードを使うので、080の先頭の0は不要）
- 参考 [【機械学習】さあ、Kaggleを始めよう！ – 初心者向けPython Kernelとは](https://www.secat-blog.net/wordpress/kaggle-getting-started-python-kernel-for-beginners/)
- つまづいてしまった場合は、本スライドAppendix「Google Colaboratoryでの実行」を参照ください

---

### Welcome to Kaggleタイタニックハンズオン

+++

### Kaggleタイタニックハンズオン 概要

- Kaggle（というコミュニティ）の
- タイタニック（というコンペ）を
- 手を動かして体験（＝ハンズオン）

+++

### ハンズオン後の姿

- 機械学習の流れをつかんだ状態
- Kaggleのコンペでは何をやるか **体験** から分かっている

+++

### アジェンダ

- 機械学習・Kaggle・タイタニックとは（10分）
- 単純なモデルを作成してみよう！（10分）
- 単純なモデルより性能のいいモデル作りに挑戦！（20分）
- まとめ（10分）

---

### Kaggleタイタニックハンズオン

- **機械学習・Kaggle・タイタニックとは**（10分）
- 単純なモデルを作成してみよう！（10分）
- 単純なモデルより性能のいいモデル作りに挑戦！（20分）
- まとめ（10分）

+++

### 導入

1. 機械学習とは
2. Kaggleとは
3. タイタニックとは

+++

### (1)機械学習とは

- **データ** と **アルゴリズム** からモデルを作る
- アルゴリズムは計算方法（データからモデルを作る手順）

+++

### モデル

- イメージ：**予測するためのルール**
- 実態は「計算式の塊」
- 人が決めるのではなく、データにアルゴリズムを適用して見出す

+++

### 一例：知っているデータから知らないデータを予測

1. 知っているデータからモデルを作る
2. モデルで知らないデータについて予測する

このあと具体化します

+++

### 人工知能とディープラーニングとの関係

- 人工知能（Artificial Intelligence）という研究分野の一領域が機械学習
- 機械学習の手法の一つがディープラーニング

+++

### 機械学習の流れ

<span class="seventy-percent-img">
![問題設定→データ収集→分析→前処理→モデル作成→モデル評価→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.002.png)
</span>

---

### (2)Kaggleとは

- データサイエンスコンペのプラットフォーム
- モデルの性能を競う
- 全世界で105000名超えが参加（2019/03/03 [アカウント数](https://www.kaggle.com/rankings)集計）

+++

### Kaggleの対象範囲

<span class="sixty-percent-img">
![問題設定→データ収集→**分析→前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.003.png)
</span>

今回体験していきます

+++

### Kaggleのコンペ 1/2

@snap[east span-50]

@box[span-100](知っているデータから知らないデータを予測することが多い)

@ul[](false)
* モデル作成用データ（知っているデータ）
* 予測対象データ（知らないデータ）
@ulend

@snapend

@snap[west span-50]

<span class="seventy-percent-img">
![「モデル」を使って「知らないデータ」について予測する](spz_Jan_titanic_handson/assets/201901kaggel_talk.007.png)
</span>

@snapend

+++

### kaggleのコンペ 2/2

- 予測対象データをモデルが予測した結果をKaggleに提出
- Kaggleに用意された「正解」から提出結果が採点され、モデルの性能にスコアがつく
    - スコアとなる指標はコンペごとに異なる
- 一番優秀なスコアのモデルを作った人（チーム）が優勝

---

### (3)タイタニックとは🛳️

- 機械学習の入門者用コンペ
    - [What is a Getting Started competition?](https://www.kaggle.com/c/titanic#frequently-asked-questions)
- 沈没したタイタニック号の乗客データを用いる
- **乗客が生存したか死亡したかを予測したい**

+++

### 「知っているデータ」と「知らないデータ」

&nbsp; | 種別 | タイタニックの場合
----- | ----- | -----
知っているデータ | モデル作成用データ | 乗客の属性 & 生存／死亡を知っている
知らないデータ | 予測対象データ | 乗客の属性のみ（生存／死亡を知らない）

+++

### 例：タイタニックの場合に取り組むこと

- 乗客の属性と生存／死亡情報からモデルを作り、
- 生存／死亡を知らない乗客について、生存／死亡を予測する（スコアとなる指標は、予測の正解率）
- ref: https://www.kaggle.com/c/titanic#evaluation

>@size[70%](It is your job to predict if a passenger survived the sinking of the Titanic or not.)
@size[70%](For each PassengerId in the test set, you must predict a 0 or 1 value for the Survived variable.)

+++

### タイタニックのイメージ

データ種別 | 年齢 | 性別 | 生死
----- | ----- | ----- | -----
モデル作成用データ | 26歳 | 男性 | 死亡
モデル作成用データ | 30歳 | 男性 | 死亡
モデル作成用データ | 28歳 | 女性 | 生存
予測対象データ | 28歳 | 男性 | ？(予測)

+++

## Are you ready? 😎

---

### Kaggleタイタニックハンズオン

- 機械学習・Kaggle・タイタニックとは（10分）
- **単純なモデルを作成してみよう！**（10分）
- 単純なモデルより性能のいいモデル作りに挑戦！（20分）
- まとめ（10分）

+++

### タイタニックコンペに参加

**全員** 操作をお願いします🙇

- ログイン後 https://www.kaggle.com/c/titanic にアクセス
- （コンペ一覧 https://www.kaggle.com/competitions から「titanic」で検索してもよい）

+++

### タイタニックコンペにJoin

![「Join Competition」→「I Understand and Accept」](spz_Jan_titanic_handson/assets/join_titanic_competition.png)

+++

### ハンズオン

- ブラウザで以下のKernel（≒ソースコード）にアクセス
  - https://www.kaggle.com/ftnext/kaggle-spzcolab-online
- Kernelを自分のアカウントにコピーします（フォークと言います）

+++

### Kernelのコピー

![「・・・」→「Fork Kernel」をクリック](spz_Jan_titanic_handson/assets/fork_kernel.png)

+++

## 準備完了です！👍

![Kernelのコピーが編集できるようになりました](spz_Jan_titanic_handson/assets/editting_kernel.png)

以降はKernelを一緒に進めます

+++

### Kernelの提出方法

- 前提：submisson.csvを作成するセルまで実行が終わった状態
- オプション：タイトルを変えたい人は変える
  - 例：「20190306_1_sex」

+++

### 1. Kernel上部の「Commit」をクリック

![](spz_Jan_titanic_handson/assets/commit_kernel.png)

+++

### 2. 現れたリンクをクリック

![outputという項目へ移動](spz_Jan_titanic_handson/assets/kaggle_kernel_go_output.png)

+++

### 3. Submit to Competition

![](spz_Jan_titanic_handson/assets/kaggle_kernel_submission.png)

+++

### 初提出、お疲れさまでした🎉

---

### Kaggleタイタニックハンズオン

- 機械学習・Kaggle・タイタニックとは（10分）
- 単純なモデルを作成してみよう！（10分）
- **単純なモデルより性能のいいモデル作りに挑戦！**（20分）
- まとめ（10分）

+++

### 単純なモデルより性能のいいモデル作りに挑戦！

- モデル作成を一緒に体験（2）：10分
- 用意した選択肢2つのうちお好きなものを実行（3）：10分

+++

### Kernel再実行 1/3

![提出した画面で上部のKernelsをクリック](spz_Jan_titanic_handson/assets/submission_results_to_kernel.jpg)

+++

### Kernel再実行 2/3

![Your Workから先ほどのKernelをクリック](spz_Jan_titanic_handson/assets/select_your_kernels.png)

+++

### Kernel再実行 3/3

![Editをクリック](spz_Jan_titanic_handson/assets/edit_committed_kernel.png)

（以降はKernelで説明します）

+++

### 0.76555超えを目指す💪

- 選択肢1,2のうち、試したい方を実行してみましょう
- Kernelを編集しながら選択肢のコードを **上から順に実行** します
- （操作が不安な方は一緒に進めましょう）

+++

## 0.76555超えた人🙋

スコアをコメントしてみてください

---

### Kaggleタイタニックハンズオン

- 機械学習・Kaggle・タイタニックとは（10分）
- 単純なモデルを作成してみよう！（10分）
- 単純なモデルより性能のいいモデル作りに挑戦！（20分）
- **まとめ**（10分）

+++

### まとめ

- ハンズオンの振り返り
- この先へ進みたい方へ

+++

### 再掲：機械学習の全体像

<span class="seventy-percent-img">
![問題設定→データ収集→分析→**前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.003.png)
</span>

+++

### 体験したこと

1. 分析（生存と関係するデータ項目を洗い出した）
2. 前処理（データは抜けや形式のために、そのままでは機械学習に持ち込めない）
3. モデル作成（わずか1行！）
4. モデル評価

+++

### 先へ進みたい方へ

- **機械学習の考え方** を学ぶ
- Pythonを学ぶ
- Pythonで使うツール（パッケージ）を学ぶ

+++

### 参考書籍 1/2

- 機械学習の考え方：『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』
- Pythonを書けるようになるには？ 入門書は豊富、[公式チュートリアル](https://docs.python.org/ja/3/tutorial/index.html)(無料)、有料のオンライン教材(PyQなど)

+++

### 参考書籍 2/2

- まずはpandas（分析・前処理）とscikit-learn（モデル作成・評価）
- 『Pythonによるあたらしいデータ分析の教科書』で入門できます
- 『[Pythonではじめる機械学習](https://www.amazon.co.jp/dp/4873117984/)』scikit-learn（実践）
- 『[pandasクックブック](https://www.amazon.co.jp/dp/425412242X)』pandas（実践）

+++

### さらに手を動かしたい方へ

- [1月ハンズオン資料](https://gitpitch.com/ftnext/2019_slides/master?p=spz_Jan_titanic_handson/)
- [3月ハンズオン資料](https://gitpitch.com/ftnext/2019_slides/master?p=spz_Mar_titanic_handson2/)
- 元にした[PyData.Tokyo Tutorial](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1)

+++

### （参考）GUIで機械学習

- 新しく言語を学ぶのは大変という方へ
- GUIで機械学習をし、考え方を学ぶことができる
- 例：[Azure Machine Learning Studio](https://studio.azureml.net/)

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### 機械学習の流れ

<span class="seventy-percent-img">
![問題設定→データ収集→分析→前処理→モデル作成→モデル評価→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.002.png)
</span>

+++

### 機械学習の流れ 1/2

1. 問題設定（課題〇〇を機械学習を使って解決しよう）
2. データ収集（機械学習で使うデータを収集）
3. **データ分析**（集めたデータの傾向を確認）
4. **前処理**（データを整え、機械学習に持ち込める形式にする）

+++

### 機械学習の流れ 2/2

5. **モデル作成**（整えたデータとアルゴリズムから）
6. **モデル評価**（作ったモデルの性能を確認し、もっとも性能のいいモデルを選抜）
7. 運用（性能のいいモデルを運用して問題解決）

+++

### Appendix: Google Colaboratoryでの実行

- Kaggleが使えない場合のハンズオン用に用意
- Googleアカウントを持っている前提
- 用意したサンプルコードはColaboratoryでも動かすことができる

+++

### Google Colaboratoryでの実行手順

1. https://colab.research.google.com/ にアクセス
2. GitHubリポジトリ https://github.com/ftnext/spzcolab_titanic の中のノートブックを開く(続くスライドで説明)

+++

### ノートブックを開く 1/2

![GitHubのタブを選び、https://github.com/ftnext/spzcolab_titanic と入力](spz_Jan_titanic_handson/assets/colab_select_notebook.png)

+++

### ノートブックを開く 2/2

![ノートブック(.ipynb)のリンクをクリック](spz_online_titanic_handson/assets/colab_select_notebook2.png)

+++

### セル実行時 1/2

![セルを初めて実行したときの警告は「このまま実行」を選択](spz_Jan_titanic_handson/assets/colab_run_cell.png)

+++

### セル実行時 2/2

![続くすべてのランタイムをリセットは「はい」を選択](spz_Jan_titanic_handson/assets/colab_run_cell2.png)

+++

# EOF
