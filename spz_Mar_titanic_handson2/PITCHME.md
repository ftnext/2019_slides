## 続・機械学習に興味ありますか？<br>Kaggle始めたいですか？<br>タイタニックでもいいですか？
#### サポーターズ勉強会 2019/03/05 nikkie

---

### [1月のタイタニックハンズオン](https://supporterzcolab.com/event/677/)続編です

![](spz_Mar_titanic_handson2/assets/jan_logo.png)

+++

### アンケート🙋‍ 1/2

- 1月のタイタニックハンズオン(2019/01/30)に来られた方
- 今回が初めての方

+++

### アンケート🙋‍ 2/2

- Pythonでデータ分析経験あり
- PythonでWebや自動化経験あり
- Python以外でデータ分析経験あり

+++

### 概要

- ハンズオン形式でKaggleのタイタニックコンペに取り組みます
- 環境構築不要。Kaggleのアカウントが必要
- Pythonのサンプルコードを組合せて、試行錯誤しましょう

+++

### 自己紹介（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 業務では、GUIで機械学習できるツールのセミナー教材作成
- Pythonを教える活動も [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳に参加
- アニメが好き（アイマス、ユーフォ）

+++

### 頼れるTAの皆さま👏

- nao_yさん
- shimakaze_softさん

---

### Kaggleのアカウント作成

**事前に作っていない人** は作成をお願いします🙇

まず https://www.kaggle.com/account/login にアクセス

+++

![お好みの登録方法で進めてください（FB, Google, Yahoo, Email）](spz_Jan_titanic_handson/assets/kaggle_register.png)

+++

### ハンズオン後の姿

- Kaggleのタイタニックコンペで機械学習を **体験** していただく
- 「機械学習はこんなことをやるのか」とつかんでいただく

+++

### このハンズオンの限界

- 機械学習の概念を詳細に説明しません
- ディープラーニングには立ち入りません

+++

## Kaggleのアカウントはできましたか？

+++

### アジェンダ（TODO：見直し）

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（30分）
- もくもくタイム：精度向上に各自挑戦（5分）
- まとめ（10分）

---

### 続・すかすかタイタニックハンズオン

TODO：見直したアジェンダを貼る

+++

### 導入

1. 機械学習とは
2. Kaggleとは
3. タイタニックとは

+++

### (1)機械学習とは

<span class="seventy-percent-img">
![データとアルゴリズムからモデル（計算式の塊）を作る](spz_Jan_titanic_handson/assets/201901kaggel_talk.001.png)
</span>

+++

### （参考）機械学習

- 教師あり学習
  - 分類（タイタニックコンペが該当）
  - 回帰
- 教師なし学習
- 強化学習

+++

### 機械学習の流れ

<span class="seventy-percent-img">
![問題設定→データ収集→分析→前処理→モデル作成→モデル評価→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.002.png)
</span>

+++

### (2)Kaggleとは

- データサイエンスコンペのプラットフォーム
- 私のイメージ「機械学習を学ぶにはKaggleがいいらしい」
- 全世界で97000名超えが参加（2019/01/18 [アカウント数](https://www.kaggle.com/rankings)集計）
- 学習コンテンツ[Kaggle Learn](https://www.kaggle.com/learn/overview)も提供

+++

### Kaggleの対象範囲

<span class="sixty-percent-img">
![問題設定→データ収集→**分析→前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.003.png)
</span>

今回体験していきます

+++

### Kaggleのコンペ 1/2

コンペでは、2つのデータが与えられる

* モデル作成用データ
* 予測対象データ

+++

### 機械学習で取り組むこと（分類の場合）

<span class="seventy-percent-img">
![「知っているデータ」から「知らないデータ」を予測したい](spz_Jan_titanic_handson/assets/201901kaggel_talk.005.png)
</span>

+++

### 「知っているデータ」から「知らないデータ」を予測 1/2

<span class="seventy-percent-img">
![「知っているデータ」から「モデル」を作る](spz_Jan_titanic_handson/assets/201901kaggel_talk.006.png)
</span>

+++

### 「知っているデータ」から「知らないデータ」を予測 2/2

<span class="seventy-percent-img">
![「モデル」を使って「知らないデータ」について予測する](spz_Jan_titanic_handson/assets/201901kaggel_talk.007.png)
</span>

+++

### 「知っているデータ」と「知らないデータ」

&nbsp; | コンペでの扱い
----- | -----
知っているデータ | モデル作成用データ
知らないデータ | 予測対象データ

+++

### kaggleのコンペ 2/2

- 予測対象データをモデルが予測した結果をKaggleに提出
- Kaggleに用意された「正解」から提出結果が採点され、モデルの性能にスコアがつく
    - スコアとなる指標はコンペごとに異なる
- 一番優秀なスコアのモデルを作った人（チーム）が優勝

+++

### (3)タイタニックとは🛳️

- 機械学習の入門者用コンペ
    - [What is a Getting Started competition?](https://www.kaggle.com/c/titanic#frequently-asked-questions)
- 沈没したタイタニック号の乗客データを用いる
- **乗客が生存したか死亡したかを予測したい**

+++

### 「知っているデータ」と「知らないデータ」

 | コンペでの扱い | タイタニックの場合
----- | ----- | -----
知っているデータ | モデル作成用データ | 生存／死亡を知っている
知らないデータ | 予測対象データ | 生存／死亡を知らない

+++

### 例：タイタニックの場合に取り組むこと

- 乗客の属性と生存／死亡情報からモデルを作る
- モデルを使って、生存／死亡を知らない乗客について、生存／死亡を予測する（スコアとなる指標は、予測の正解率）
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

### すかすかタイタニックハンズオン

+++

### ハンズオン（30分）

1. 分析(10分)
2. 前処理、モデル作成、評価(15分)
3. 精度を上げるためのアプローチの紹介（5分）

+++

### タイタニックコンペに参加

**全員** 操作をお願いします🙇

- ログイン後 https://www.kaggle.com/competitions にアクセス
- （上部の「Competition」のクリックでもOK）

+++

### 「titanic」でコンペを検索🔍

![検索欄にtitanicと入力](spz_Jan_titanic_handson/assets/1_search_titanic_competition.png)

+++

### タイタニックコンペにJoin

![「Join Competition」→「I Understand and Accept」](spz_Jan_titanic_handson/assets/join_titanic_competition.png)

+++

### ハンズオン

- ブラウザで以下のKernel（≒ソースコード）にアクセス
  - TODO：リンクを貼る
- Kernelを自分のアカウントにコピーします（フォークと言います）

+++

### Kernelのコピー

![「・・・」→「Fork Kernel」をクリック](spz_Jan_titanic_handson/assets/fork_kernel.png)

+++

## 準備完了です！👍

![Kernelのコピーが編集できるようになりました](spz_Jan_titanic_handson/assets/editting_kernel.png)

以降はKernelを一緒に進めます

+++

### Kernelの概要

1. 分析
2. モデル作成
3. 試行錯誤に使うコード

TODO：以下をソースコードに盛り込む

4つの特徴量に絞って扱うとする
（欠損値は確認しておいて、除いて可視化する）

### 可視化

- 生存者の特徴を見ていく
- 性別との関係（女性は助かっている）
- 年齢の分布を性別ごとに見る
- 性別ごとの年齢の分布+生存死亡の塗り分け
- 生存とPclassとの関係を見る（TODO：matplotlibのコード確認）
- 年齢の分布を性別・Pclassごとに見る
- 生存とEmbarkedとの関係を見る（TODO：matplotlibのコード確認）
- 年齢の分布を性別・Embarkedごとに見る

### モデル作成

- 前処理：AgeとEmbarkedの欠損を埋める
- 前処理：カテゴリカル変数の変換（Sex、Embarked）
- モデル作成用データを2つに分ける
- ロジスティック回帰でモデル作成
- 性能評価し、提出

（TODO終わり）

### Kernelの提出方法

- 前提：submisson.csvを作成するセルまで実行が終わった状態
- オプション：タイトルを変えたい人は変える
  - 例：「first_submission_20190305」

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

+++

### 提出練習用データを試す

- 試しに提出することができる生死予測データ
- ここに提出したkernelがあります（nikkieだけで試します）

+++

### 提出練習用データ

- 性能：0.76555 😳
- ロジックはシンプル。**女性が助かり、男性が死亡と予測**

---

### 0.76555超えを目指す

- サンプルコードを組合せてみましょう
- 先ほどCommitしたKernelを編集しながら **上から再実行** します

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

TODO：試行錯誤するコード
年齢の欠損値の埋め方
別のアルゴリズム

+++

## もくもくタイムです！

## 精度向上に挑戦💪

+++

## 0.76555超えた人🙋

---

### すかすかタイタニックハンズオン

+++

### まとめ

- ハンズオンの振り返り
- 「Kaggleを始めてからどんなコンペに取り組めばいいか」

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

### Kaggleの苦楽

- 楽：分析→前処理を工夫するアイデア→試してスコアが上がる
  - 面白いのは分析（人が仮説を立てて行う領域）
- 苦：工夫をいくつか試すも、スコアが上がらず
  - ランダムフォレストというアルゴリズムでモデルを作り、0.727というスコアからはじめました

---

### Kaggleへの取り組み方（案）

- 今回はじめて取り組んだ方
  - 引き続きタイタニックコンペ（目標 accuracy 80%）
- タイタニックは満足という方
  - 開催中の興味あるコンペに挑戦

+++

### コンペに取り組むときのポイント

- 先人のKernelを写経し、変更を試す
- そのために、機械学習の考え方をつかもう

+++

### 先人のKernel

![投票数が多いもの、またはスコアが高いものに注目しましょう。また、言語で絞り込めます](spz_Mar_titanic_handson2/assets/titanic_kernels.png)

+++

### 機械学習の考え方を学ぶ

- コードはKernelに豊富にある（コピーすれば動かせる）
- 機械学習の考え方（例：モデル作成用データの分割）をつかみ、コードを自由に読み書きしよう
- 参考書籍『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』(2018)

+++

### 開催中のコンペに参加

- 興味もてるものを：[**銀行の取引予測**](https://www.kaggle.com/c/santander-customer-transaction-prediction)、[電力網の故障予測](https://www.kaggle.com/c/vsb-power-line-fault-detection)、[バスケの試合結果予測](https://www.kaggle.com/c/mens-machine-learning-competition-2019)
- 評価が高いKernel、スコアが高いKernelの写経から
- ref: 2018/05 [[入門者向け] Kaggle入門](https://supporterzcolab.com/event/380/)

+++

### 写経中の私の未来（Python前提）

<span class="seventy-percent-img">
![pandas, matplotlib, scikit-learnの進んだ使い方や、ニューラルネットワークなどへのキャッチアップで情報氾濫状態](spz_Mar_titanic_handson2/assets/201903kaggle_talk.001.png)
</span>

+++

### 優先度と身につける範囲を決める（案）

1. pandas（分析・前処理）とscikit-learn（モデル作成・評価）に入門する
2. pandasとscikit-learnでやりたいことができる状態（中級者）を目指す
3. scikit-learnにないアルゴリズム（LightGBMなど）やmatplotlib（分析での可視化）

+++

### 書籍紹介（勉強中です）

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』pandas, matplotlib, scikit-learnに入門
- 『[Pythonではじめる機械学習](https://www.amazon.co.jp/dp/4873117984/)』scikit-learn（実践）
- 『[pandasクックブック](https://www.amazon.co.jp/dp/425412242X)』pandas（実践）
- Webドキュメント：（例）[LightGBM](https://lightgbm.readthedocs.io/en/latest/)

+++

### 心構え

- 本などでの情報収集と先人のKernelの両輪で取り組む
- 英語を怖がらない（Google翻訳）
- Kagglerから情報を入手しよう（例 [カレーちゃん](https://twitter.com/currypurin)さん）
- 時間の確保（他は手を出せなくなる）

+++

### 仲間と取り組む（ジャストアイデア）

- サポーターズさんとColabして、Kaggleもくもく部屋みたいなのができないだろうか？
- サポーターズKaggle興味ある人Slack（学び方の情報交換）
- Colabもくもく会に集まる
- モブでPlaygroundコンペに取り組む（前回の感想から）

+++

### 参考文献（ハンズオン準備に当たり）

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』pydatatext（ベースにしました）
- PyData.Tokyo Tutorial [分析パート](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1/blob/master/pydatatokyo_tutorial_dh.ipynb) [モデル作成パート](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1/blob/master/pydatatokyo_tutorial_ml.ipynb)（タイタニックコンペを扱った先行事例）
- 『[PythonユーザのためのJupyter 実践 入門](https://www.amazon.co.jp/dp/4774192236/)』matplotlibの解説を参照

+++

### 宣伝：技術書典6でアウトプットします

- サークル「サポーターズCoLab」にて合同誌に参加
- ハンズオンの先の話として、交差検証・グリッドサーチを取り上げます
- PyData.Tokyo Tutorial で学んだことのアウトプットです

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix

- ハンズオンソースコードへの補足情報
- タイタニック号沈没事故について（分析の裏付け）
- Google Colaboratoryでの実行

+++

### （参考）`train_test_split` 1/3

<span class="seventy-percent-img">
![モデル作成用データをランダムに2つに分ける](spz_Jan_titanic_handson/assets/201901kaggel_talk.008.png)
</span>

+++

### （参考）`train_test_split` 2/3

<span class="seventy-percent-img">
![2つに分けた片方からモデルを作る](spz_Jan_titanic_handson/assets/201901kaggel_talk.009.png)
</span>

+++

### （参考）`train_test_split` 3/3

<span class="seventy-percent-img">
![2つに分けた残りでモデルの性能を評価する](spz_Jan_titanic_handson/assets/201901kaggel_talk.010.png)
</span>

+++

### matplotlib figureとaxes

+++

### さらに工夫できる 1/2

- 連続値（AgeやFare）をいくつかのカテゴリに分ける
- 年齢の小さいところで助かっている（4歳以下）
  - → Nameを加工してTitle

+++

### さらに工夫できる 2/2

- 特徴量を作る
    - Aloneかどうか（SibSpとParchを加工する）
    - Pclass と Age（カテゴリ）の積
- 詳しくは[可視化の参考にしたkernel参照](https://www.kaggle.com/startupsci/titanic-data-science-solutions)

---

### タイタニック号沈没事故

- Wikipedia [タイタニック号沈没事故](https://ja.m.wikipedia.org/wiki/%E3%82%BF%E3%82%A4%E3%82%BF%E3%83%8B%E3%83%83%E3%82%AF%E5%8F%B7%E6%B2%88%E6%B2%A1%E4%BA%8B%E6%95%85)
- 1912年4月の海難事故
- イギリス・サウサンプトンからアメリカ・ニューヨークへの航海中、氷山に衝突
- 2224人を乗せており、1513人(**68%**)が死亡

+++

### （おまけ）タイタニック裏話

先のWikipediaを確認したところ・・・

- 救命ボートの数が全員分ない -> 女性と子供優先
- 客室係がさばく乗客の数が等級によって違う
- 三等船室からデッキまでたどり着けず（客室係と言葉が通じない問題）

---

### Google Colaboratoryでの実行

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

![ノートブック(.ipynb)のリンクをクリック](spz_Jan_titanic_handson/assets/colab_select_notebook2.png)

+++

### セル実行時 1/2

![セルを初めて実行したときの警告は「このまま実行」を選択](spz_Jan_titanic_handson/assets/colab_run_cell.png)

+++

### セル実行時 2/2

![続くすべてのランタイムをリセットは「はい」を選択](spz_Jan_titanic_handson/assets/colab_run_cell2.png)

+++

# EOF
