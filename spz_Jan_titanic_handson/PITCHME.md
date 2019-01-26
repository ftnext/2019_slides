## 機械学習に興味ありますか？
## Kaggle始めたいですか？
## タイタニックでもいいですか？
#### サポーターズ勉強会 2019/01/30 nikkie

---

### アンケート

前処理、欠損値

1. 何のことかわかる方？
2. 聞いたことがある方？

**注**: このあと説明し、体験もしていただくので、今はわからなくても問題ありません

+++

### 概要

- ハンズオン形式でKaggleのタイタニックコンペに取り組みます
- 環境構築不要。Kaggleのアカウントが必要
- Pythonのサンプルコードを組合せて、試行錯誤しましょう

+++

### Kaggleのアカウント作成

事前に作っていない人向け

1. https://www.kaggle.com/account/login にアクセス
2. お好みの登録方法で進めてください（FB, Google, Yahoo, Email）

+++

### タイタニックコンペに参加

1. ログイン後 https://www.kaggle.com/competitions にアクセス（上部の「Competition」）
2. 「titanic」で検索
3. タイタニックコンペにJoin

参考情報：Qiita [Kaggle事始め](https://qiita.com/taka4sato/items/802c494fdebeaa7f43b7)

+++

### 「titanic」でコンペを検索

![タイタニックコンペを検索](spz_Jan_titanic_handson/assets/1_search_titanic_competition.png)

+++

### タイタニックコンペにJoin

![](spz_Jan_titanic_handson/assets/join_titanic_competition.png)

+++

### 自己紹介（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 業務ではマーケティング(Google Analyticsなど)
- Pythonを教える活動も [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳に参加
- アニメが好き（アイマス、ユーフォ）

+++

### ハンズオン後の姿

- Kaggleのタイタニックコンペで機械学習を体験していただく
- 「機械学習はこんなことをやるのか」とつかんでいただく
- 機械学習の勉強に進むもよし、ハンズオンで満足してもよし

+++

### このハンズオンの限界

- 機械学習の概念を詳細に説明しません
- ディープラーニングには立ち入りません

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

データとアルゴリズム→モデル（モデル＝「計算式の塊」）

+++

### （参考）機械学習

タイタニックコンペは、教師あり学習・分類です

- 教師あり学習
  - 分類
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

時間の都合により分析は省略しています。

+++

### (3)タイタニックとは

- 機械学習の入門者用コンペ
    - [What is a Getting Started competition?](https://www.kaggle.com/c/titanic#frequently-asked-questions)
- 乗客が生存か死亡かを予測したい
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

### kaggleのコンペ 2/2

- モデルがテスト用データについて推測した結果をKaggleに提出
- Kaggleには「正解」が用意されていて、提出結果からモデルの性能が評価される
    - 性能評価に使う指標はコンペごとに異なる
    - タイタニックの場合：生存／死亡を正しく予想できた割合
- 性能が一番高いモデルを作った人（チーム）が優勝

+++

### タイタニックのイメージ

データ種別 | 年齢 | 性別 | 生死
----- | ----- | ----- | -----
学習用データ | 26歳 | 男性 | 死亡
学習用データ | 30歳 | 男性 | 死亡
学習用データ | 28歳 | 女性 | 生存
テスト用データ | 28歳 | 男性 | ？(推測)

+++

## Are you ready?

## （アカウントはできましたか？）

---

### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- <div class="kaggle-color-highlight">ハンズオン：手を動かしてタイタニックコンペに参加（20分）</div>
- 座学：精度を上げるためのアプローチの紹介（5分）
- もくもくタイム：精度向上に各自挑戦（15分）
- まとめ（10分）

+++

### ハンズオン

ブラウザで2つの操作

1. サンプルコードのGistにアクセス
    - https://gist.github.com/ftnext/34d8ad1bacbd7b928915c12599af9f92
    - titanic_handson_sample_code.ipynb を使います
2. KaggleでKernelを立ち上げる（このあと一緒にやります）

+++

https://www.kaggle.com/c/titanic

![Kernelをクリック](spz_Jan_titanic_handson/assets/2_go_titanic_kernel.png)

+++

![New Kernelをクリック](spz_Jan_titanic_handson/assets/3_go_new_kernel.png)

+++

![Notebookを選択](spz_Jan_titanic_handson/assets/4_choose_notebook.png)

+++

ここから先はソースコードに寄せる
ソースコードはバッサリ削る
必要なところだけスライドにする

+++

### 大まかな流れ

機械学習ではこう進みますという図を入れる（サンプルコードに寄せる）
前処理はなぜ必要か。そのままでは機械学習に持ち込めない（抜けがある。扱いづらい「整っていないデータ」）

1. `train_df`からモデルを作る
    - 前処理
        - 欠損値処理
        - カテゴリ変数の扱い
    - 性能確認
2. 作成したモデルで`test_df`について予測する

+++

### モデル作成のポイント（図にする）

- `test_df`について予測する前に、どの程度の性能のモデルなのか確認したい
- そこで、`train_df`をランダムに2つに分ける（`train_test_split`）
    - `train_df`のうち7割でモデルを作る
    - 残りの3割でモデルの性能を評価する

+++

### （参考）モデル作成のポイント

- 今回はすぐ提出するが、別のモデルを作ったときに、モデルの性能が芳しく無ければ提出しないと判断できる ←ここの文章の見直し

+++

TODO：提出方法を追加

タイトル入れる「first_submission_20190130」
commitする（コードが実行される）
リンクが現れるのでクリックする
下にスクロールしてsubmission

+++

### 提出練習用データセット

- 試しに提出することができるデータセット
- 性能：0.76555
- ロジックはシンプル。女性が助かり、男性が死亡と予測

---

### 0.76555超えを目指す

サンプルコードを組合せてみましょう

ノートブックは再実行します

- Ageの欠損の埋め方を見直す
- AgeとFareを数段階のカテゴリに変換する（やらない）
- モデルのアルゴリズムを変える（SVM、ランダムフォレスト）どういうものかざっくり説明

+++

## もくもくタイムです！

## 精度向上に挑戦💪

+++

## 0.76555超えた人🙋

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
