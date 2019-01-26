## 機械学習に興味ありますか？
## Kaggle始めたいですか？
## タイタニックでもいいですか？
#### サポーターズ勉強会 2019/01/30 nikkie

---

### アンケート🙋‍

- 「前処理」「欠損値」が何かわかる
- 「前処理」「欠損値」を聞いたことがある

**注**: このあと説明し、体験もしていただくので、今は用語がわからなくても問題ありません

+++

### 概要

- ハンズオン形式でKaggleのタイタニックコンペに取り組みます
- 環境構築不要。Kaggleのアカウントが必要
- Pythonのサンプルコードを組合せて、試行錯誤しましょう

+++

### Kaggleのアカウント作成

**事前に作っていない人** は作成をお願いします🙇

まず https://www.kaggle.com/account/login にアクセス

+++

![お好みの登録方法で進めてください（FB, Google, Yahoo, Email）](spz_Jan_titanic_handson/assets/kaggle_register.png)

---

### 自己紹介（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 業務ではマーケティング(Google Analyticsなど)
- Pythonを教える活動も [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳に参加
- アニメが好き（アイマス、ユーフォ）

+++

### ハンズオン後の姿

- Kaggleのタイタニックコンペで機械学習を **体験** していただく
- 「機械学習はこんなことをやるのか」とつかんでいただく
- 機械学習の勉強に進むもよし、ハンズオンで満足してもよし

+++

### このハンズオンの限界

- 機械学習の概念を詳細に説明しません
- ディープラーニングには立ち入りません

+++

## Kaggleのアカウントはできましたか？

+++

### アジェンダ

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（20分）
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（15分）
- まとめ（10分）

---

### すかすかタイタニックハンズオン

- <div class="kaggle-color-highlight">導入：機械学習／Kaggle／タイタニック（10分）</div>
- ハンズオン：手を動かしてタイタニックコンペに参加（20分）
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（15分）
- まとめ（10分）

+++

### 導入

1. 機械学習とは
2. Kaggleとは
3. タイタニックとは

+++

### (1)機械学習とは

図：データとアルゴリズム→モデル（モデル＝「計算式の塊」）

+++

### （参考）機械学習

- 教師あり学習
  - 分類（タイタニックコンペが該当）
  - 回帰
- 教師なし学習
- 強化学習

+++

### 機械学習の流れ

図：データ収集→分析→前処理→モデル作成→モデル評価→運用

+++

### (2)Kaggleとは

- データサイエンスコンペのプラットフォーム
- 私のイメージ「機械学習を学ぶにはKaggleがいいらしい」
- 全世界で97000名超えが参加（2019/01/18 [アカウント数](https://www.kaggle.com/rankings)集計）
- 学習コンテンツ[Kaggle Learn](https://www.kaggle.com/learn/overview)も提供

+++

### Kaggleの対象範囲

図：データ収集→**分析→前処理→モデル作成→モデル評価**→運用

+++

### 今回のハンズオンの範囲

図：データ収集→分析→**前処理→モデル作成→モデル評価**→運用

このハンズオンでは、**分析は省略** しています。

+++

### (3)タイタニックとは🛳️

- 機械学習の入門者用コンペ
    - [What is a Getting Started competition?](https://www.kaggle.com/c/titanic#frequently-asked-questions)
- **乗客が生存したか死亡したかを予測したい**
- 沈没したタイタニック号の乗客データからモデル作成

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

「知っているデータ」から「知らないデータ」を推測したい

 | コンペでの扱い | タイタニックの場合
----- | ----- | -----
知っているデータ | 学習用データ | 生存／死亡を知っている
知らないデータ | テスト用データ | 生存／死亡を知らない

+++

### 「知っているデータ」から「知らないデータ」を推測

- 「知っているデータ」から「モデル」を作る
- 「モデル」を使って「知らないデータ」について推測する
- モデルは「計算式の塊」（pydatatext）

+++

### 例：タイタニックの場合に取り組むこと

- 乗客の属性と生存／死亡情報からモデルを作る
- モデルを使って、生存／死亡を知らない乗客について、生存／死亡を推測する
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
テスト用データ | 28歳 | 男性 | ？(推測)

+++

### kaggleのコンペ 2/2

- テスト用データについてモデルが推測した結果をKaggleに提出
- Kaggleには「正解」が用意されていて、提出結果からモデルの性能が評価される
    - 性能評価に使う指標はコンペごとに異なる
    - タイタニックの場合：生存／死亡の正解率
- 性能が一番高いモデルを作った人（チーム）が優勝

+++

## Are you ready? 😎

---

### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- <div class="kaggle-color-highlight">ハンズオン：手を動かしてタイタニックコンペに参加（20分）</div>
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（15分）
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
- 自分のアカウントにコピーして、お手元で動かします

+++

### Kernelのコピー

![「・・・」→「Fork Kernel」をクリック](spz_Jan_titanic_handson/assets/fork_kernel.png)

+++

## 準備完了です！👍

![Kernelのコピーが編集できるようになりました](spz_Jan_titanic_handson/assets/editting_kernel.png)

以降はKernelを一緒に進めます

+++

### 大まかな流れ（TODO:位置変え）

機械学習ではこう進みますという図を入れる（サンプルコードに寄せる）
前処理はなぜ必要か。そのままでは機械学習に持ち込めない（抜けがある。扱いづらい「整っていないデータ」）体験後の言語化としてみるか

1. `train_df`からモデルを作る
    - 前処理
        - 欠損値処理
        - カテゴリ変数の扱い
    - 性能確認
2. 作成したモデルで`test_df`について予測する

+++

### モデル作成のポイント（TODO:図にする）

- `test_df`について予測する前に、どの程度の性能のモデルなのか確認したい
- そこで、`train_df`をランダムに2つに分ける（`train_test_split`）
    - `train_df`のうち7割でモデルを作る
    - 残りの3割でモデルの性能を評価する

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

### Kernel再実行

![Editをクリック](spz_Jan_titanic_handson/assets/edit_committed_kernel.png)

（以降はKernelで説明します）

+++

## もくもくタイムです！

## 精度向上に挑戦💪

+++

## 0.76555超えた人🙋

+++

## 0.80超えた人🙋 👏

---

### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（20分）
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（15分）
- <div class="kaggle-color-highlight">まとめ（10分）</div>

+++

### まとめ

- さらなる工夫の紹介
- ハンズオン後の機械学習学び方案

+++

### 機械学習の全体像

実は可視化が必要

- モデル構築に使うデータを選抜する（可視化）
    - 人が仮説を立てて行う領域
- モデルを構築する（今回体験）

+++

TODO:今後学ぶ上でのキーワードを共有

+++

### さらに工夫できる

- 年齢の小さいところで助かっている（4歳以下）Nameを加工してTitle
- 特徴量を作る
    - Aloneかどうか（SibSpとParchを加工する）
    - Pclass と Age（カテゴリ）の積
- 詳しくは[可視化の参考にしたkernel参照](https://www.kaggle.com/startupsci/titanic-data-science-solutions)

+++

### nikkie（エンジニア出身）の考え

- データサイエンティストとエンジニアが協働できれば素敵
- エンジニアは性能のいい機械学習モデルが作れなくても協働できる
    - 機械学習モデルをAPIにして他のアプリと連携
- アプリにAIを組み込むなら、クラウドベンダー公開の高性能な人工知能APIを使ってもいい
    - 例: Microsoft Cognitive Services

データサイエンティストはここ。エンジニアはここ

+++

### Follow your heart

- 機械学習体験、楽しかった😁
    - ハンズオンと同様のコードが書ける状態を目指してみては？（可視化や機械学習の考え方を学ぶ）
- 機械学習、意外とツライ。。😢
    - アプリケーションにできあいのモデルや人工知能APIを組み込めるように手を動かしてみては？

+++

### 今後の学習に向けて

- タイタニックは「教師あり学習」「分類問題」
- モデルを構築する前の可視化
- 実務では交差検証して性能評価
- accuracy以外の性能評価指標もある

+++

### 参考書籍（ハンズオンを作るに当たり）

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』(2018)
    - ざっとつかめる。説明がわかりやすい
- 『Python機械学習プログラミング』（現在は[2版](https://www.amazon.co.jp/dp/4295003379)）
    - 機械学習の概念について詳細な説明

+++

### 充実のオンライン教材👀

- Kaggle Learn
- [Coursera | Machine Learning](https://ja.coursera.org/lecture/machine-learning/what-is-machine-learning-Ujm7v)
- [Amazon | Machine Learning](https://aws.amazon.com/jp/training/learning-paths/machine-learning/)
- [Google | Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course/ml-intro)

「手を出したいな」と思っています

+++

参考文献

PyData
noteさん

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
- 可視化コードはGistの titanic_handson_visualization.ipynb 参照
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
