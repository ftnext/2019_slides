## 機械学習に興味ありますか？
## Kaggle始めたいですか？
## タイタニックでもいいですか？
#### サポーターズ勉強会 2019/01/30 nikkie

---

### アンケート🙋‍

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
- jbkingさん
- Fumiさん
- canzawaさん

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

### アジェンダ

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（25分）
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（10分）
- まとめ（10分）

---

### すかすかタイタニックハンズオン

- <div class="kaggle-color-highlight">導入：機械学習／Kaggle／タイタニック（10分）</div>
- ハンズオン：手を動かしてタイタニックコンペに参加（25分）
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（10分）
- まとめ（10分）

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

+++

### 今回のハンズオンの範囲

<span class="seventy-percent-img">
![問題設定→データ収集→分析→**前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.004.png)
</span>

このハンズオンでは、**分析は省略** しています。

+++

### (3)タイタニックとは🛳️

- 機械学習の入門者用コンペ
    - [What is a Getting Started competition?](https://www.kaggle.com/c/titanic#frequently-asked-questions)
- 沈没したタイタニック号の乗客データを用いる
- **乗客が生存したか死亡したかを予測したい**

+++

### タイタニックのイメージ

年齢 | 性別 | 生死
----- | ----- | -----
26歳 | 男性 | 死亡
30歳 | 男性 | 死亡
28歳 | 女性 | 生存
28歳 | 男性 | ？(予測したい)

+++

### Kaggleのコンペ 1/2

コンペでは、2つのデータが与えられる

- 学習用データ
- テスト用データ

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

 | コンペでの扱い | タイタニックの場合
----- | ----- | -----
知っているデータ | 学習用データ | 生存／死亡を知っている
知らないデータ | テスト用データ | 生存／死亡を知らない

+++

### 例：タイタニックの場合に取り組むこと

- 乗客の属性と生存／死亡情報からモデルを作る
- モデルを使って、生存／死亡を知らない乗客について、生存／死亡を予測する
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

### kaggleのコンペ 2/2

- テスト用データについてモデルが予測した結果をKaggleに提出
- Kaggleには「正解」が用意されていて、提出結果からモデルの性能が評価される
    - 性能評価に使う指標はコンペごとに異なる
    - タイタニックの場合：生存／死亡の正解率
- 性能が一番高いモデルを作った人（チーム）が優勝

+++

## Are you ready? 😎

---

### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- <div class="kaggle-color-highlight">ハンズオン：手を動かしてタイタニックコンペに参加（25分）</div>
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（10分）
- まとめ（10分）

+++

### タイタニックコンペに参加

**全員** 操作をお願いします🙇

- ログイン後 https://www.kaggle.com/competitions にアクセス
- （上部の「Competition」のクリックでもOK）

参考情報：Qiita [Kaggle事始め](https://qiita.com/taka4sato/items/802c494fdebeaa7f43b7)

+++

### 「titanic」でコンペを検索🔍

![検索欄にtitanicと入力](spz_Jan_titanic_handson/assets/1_search_titanic_competition.png)

+++

### タイタニックコンペにJoin

![「Join Competition」→「I Understand and Accept」](spz_Jan_titanic_handson/assets/join_titanic_competition.png)

+++

### ハンズオン

- ブラウザで以下のKernel（≒ソースコード）にアクセス
  - https://www.kaggle.com/ftnext/kaggle-spzcolab-201901
- Kernelを自分のアカウントにコピーします（フォークと言います）

+++

### Kernelのコピー

![「・・・」→「Fork Kernel」をクリック](spz_Jan_titanic_handson/assets/fork_kernel.png)

+++

## 準備完了です！👍

![Kernelのコピーが編集できるようになりました](spz_Jan_titanic_handson/assets/editting_kernel.png)

以降はKernelを一緒に進めます

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

### Kernelの提出方法

- 前提：submisson.csvを作成するセルまで実行が終わった状態
- オプション：タイトルを変えたい人は変える
  - 例：「first_submission_20190130」

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

![提出した画面で上部のKernelsをクリック](spz_Jan_titanic_handson/assets/submission_results_to_kernel.png)

+++

### Kernel再実行 2/3

![Your Workから先ほどのKernelをクリック](spz_Jan_titanic_handson/assets/select_your_kernels.png)

+++

### Kernel再実行 3/3

![Editをクリック](spz_Jan_titanic_handson/assets/edit_committed_kernel.png)

（以降はKernelで説明します）

+++

## もくもくタイムです！

## 精度向上に挑戦💪

+++

## 0.76555超えた人🙋

---

### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（25分）
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（10分）
- <div class="kaggle-color-highlight">まとめ（10分）</div>

+++

### まとめ

- 分析について
- さらなる工夫の紹介
- Kaggleの苦楽
- ハンズオン後の機械学習学び方案

+++

### 再掲：機械学習の全体像

<span class="seventy-percent-img">
![問題設定→データ収集→分析→**前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.004.png)
</span>

+++

### 体験したこと

1. 前処理（データは抜けや形式のために、そのままでは機械学習に持ち込めない）
2. モデル作成
3. モデル評価

+++

### 実は、面白いのは「分析」

- 今回の体験では、使うデータは決まっていた
- **分析** では、モデル作成に使うデータを選抜する
    - データを可視化する
    - 人が仮説を立てて行う領域

+++

### 分析の参考：PyData.Tokyo Tutorial

- [分析パート](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1/blob/master/pydatatokyo_tutorial_dh.ipynb)
- [モデル作成パート](https://github.com/PyDataTokyo/pydata-tokyo-tutorial-1/blob/master/pydatatokyo_tutorial_ml.ipynb)

Kernelにコピペして実行してみては？

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

### Kaggleの苦楽

- 楽：分析→工夫アイデア→試してスコアが上がる
- 苦：工夫をいくつか試すも、スコアが上がらず
  - ランダムフォレストというアルゴリズムでモデルを作り、0.727というスコアからはじめました

+++

### Follow your heart

- 機械学習体験、楽しかった😁
    - 機械学習の考え方を学びつつコンペに参加してみては？
- 機械学習、意外とツライ。。😢
    - 機械学習には立ち入らないという姿勢でももちろんOK

+++

### 機械学習の考え方を学ぶ

- コードは豊富にある（コピーすれば動かせる）
- 大事なのは、機械学習の考え方（例：学習用データ、テスト用データ）
- 考え方を掴んで、コードを自由に読み書きしよう

+++

### 今後の学習に向けて（キーワード紹介）

- タイタニックは「教師あり学習」「分類問題」
- 実務では交差検証して性能評価
- accuracy以外の性能評価指標もある
- モデル評価ではハイパーパラメタを調整する

+++

### 機械学習せずに機械学習をアプリに組み込む 1/2

- 前提：Webエンジニア視点からの意見です
- データサイエンティストとの協働
    - データサイエンティストは性能のいいモデルを作る
    - Webエンジニアはモデルをアプリに組み込む（APIにする）

+++

### 機械学習せずに機械学習をアプリに組み込む 2/2

- クラウドベンダーが高性能なモデルをAPIとして公開している
- APIを呼ぶだけで、モデルの予測結果を利用できる
- 例: Microsoft Cognitive Services

+++

### 参考書籍（ハンズオンを作るに当たり）

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』(2018) pydatatext
    - ざっとつかめる。説明がわかりやすい
- 『Python機械学習プログラミング』（現在は[2版](https://www.amazon.co.jp/dp/4295003379)）
    - 機械学習の概念について詳細な説明

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix

- タイタニック号沈没事故の情報
- 特徴量選定のための可視化

+++

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

### 特徴量選定のための可視化

モデル構築前にやる作業のイメージの共有（全ての特徴量について考える）

- 生存／死亡を判断するのに使えそうな特徴量を選びたい
- **本来は可視化してから特徴量を選択** しますが、ここでは天下り（よさそうと言われている特徴量を可視化）です
- 可視化コードは[Gist](https://gist.github.com/ftnext/34d8ad1bacbd7b928915c12599af9f92)の titanic_handson_visualization.ipynb 参照
- [特徴量の選択の参考になるkernelはこちら](https://www.kaggle.com/startupsci/titanic-data-science-solutions)

+++

### PclassとSurvived

Pclass=1と3に注目

<span class="visualize-result-img">
![](spz_Jan_titanic_handson/assets/5_pclass_count.png)
</span>

+++

### SexとSurvived

男性と女性で生存率が大きく違う

<span class="visualize-result-img">
![](spz_Jan_titanic_handson/assets/6_sex_count.png)
</span>

+++

### AgeとSurvived

生存率が異なる年齢層がある

![](spz_Jan_titanic_handson/assets/7_age_count.png)

+++

### SibSpとSurvived

SibSp=1に注目

<span class="visualize-result-img">
![](spz_Jan_titanic_handson/assets/8_sibsp_count.png)
</span>

+++

### ParchとSurvived

Parch=1と2に注目

<span class="visualize-result-img">
![](spz_Jan_titanic_handson/assets/9_parch_count.png)
</span>

+++

### FareとSurvived

死亡者が多い運賃の範囲がある

![](spz_Jan_titanic_handson/assets/10_fare_survived.png)

+++

### EmbarkedとSurvived

Embarked=SとCに注目

<span class="visualize-result-img">
![](spz_Jan_titanic_handson/assets/11_embarked_count.png)
</span>

+++

### EOF
