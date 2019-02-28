## 続・機械学習に興味ありますか？<br>Kaggle始めたいですか？<br>タイタニックでもいいですか？
#### サポーターズ勉強会 2019/03/05 nikkie

---

タイタニックハンズオン続編です

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
- 業務ではマーケティング(Google Analyticsなど)
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
- ハンズオン：手を動かしてタイタニックコンペに参加（25分）←10分分析+15分モデル
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（10分）
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

<span class="seventy-percent-img">
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

 | コンペでの扱い
----- | -----
知っているデータ | モデル作成用データ
知らないデータ | 予測対象データ

+++

### kaggleのコンペ 2/2

- 予測対象データをモデルが予測した結果をKaggleに提出
- Kaggleには「正解」が用意されていて、提出結果が採点されるからモデルの性能が評価される
    - モデルの性能にスコアがつく（スコアとなる指標はコンペごとに異なる）
- 性能が一番高いモデルを作った人（チーム）が優勝

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
- モデルを使って、生存／死亡を知らない乗客について、生存／死亡を予測する（スコアとなる指標は、生存／死亡の正解率）
- ref: https://www.kaggle.com/c/titanic#evaluation

>It is your job to predict if a passenger survived the sinking of the Titanic or not.
For each PassengerId in the test set, you must predict a 0 or 1 value for the Survived variable.

+++

### タイタニックのイメージ

データ種別 | 年齢 | 性別 | 生死
----- | ----- | ----- | -----
学習用データ | 26歳 | 男性 | 死亡
学習用データ | 30歳 | 男性 | 死亡
学習用データ | 28歳 | 女性 | 生存
テスト用データ | 28歳 | 男性 | ？(予測)

+++

## Are you ready? 😎

---

### すかすかタイタニックハンズオン

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

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix

+++

### （参考）`train_test_split` 1/3

<span class="seventy-percent-img">
![学習用データをランダムに2つに分ける](spz_Jan_titanic_handson/assets/201901kaggel_talk.008.png)
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

+++

# EOF
