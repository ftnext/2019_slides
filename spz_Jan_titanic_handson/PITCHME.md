## 機械学習に興味ありますか？
## Kaggle始めたいですか？
## タイタニックでもいいですか？
#### サポーターズ勉強会 2019/01/30 nikkie

---

### TL; DR

- ハンズオン形式でKaggleのタイタニックコンペに取り組みます
- 環境構築不要。Kaggleのアカウントが必要
- Pythonのサンプルコードを組合せて、試行錯誤しましょう
- このスライドの短縮URL：（しばらく出しておきたい）

+++

### ハンズオン後の姿

- 「機械学習はこんなことをやるのか」
- 機械学習の勉強に進むもよし、ハンズオンで満足してもよし
- 興味を持った機械学習を体験した後の自分の気持ちに正直に
- このスライドの短縮URL：（しばらく出しておきたい）

+++

### このハンズオンで扱わないもの

- 機械学習の概念を詳細に説明しません
- すべての前処理を扱うわけではありません
- 性能の確認は甘いです（交差検証を扱いません）
- ディープラーニングには立ち入りません
- このスライドの短縮URL：（しばらく出しておきたい）

+++

### Kaggleのアカウント作成

1. https://www.kaggle.com/account/login にアクセス
2. お好みの登録方法で進めてください（FB, Google, Yahoo, Email）

このスライドの短縮URL

+++

### タイタニックコンペに参加

![タイタニックコンペを検索](spz_Jan_titanic_handson/assets/1_search_titanic_competition.png)

このスライドの短縮URL

+++

### タイタニックコンペに参加

1. ログイン後 https://www.kaggle.com/competitions にアクセス（上部の「Competition」）
2. 「titanic」で検索

参考情報：Qiita [Kaggle事始め](https://qiita.com/taka4sato/items/802c494fdebeaa7f43b7)

+++

### 自己紹介（About nikkie）

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 業務ではマーケティング(Google Analyticsなど)
- Pythonを教える活動も [Django Girls Tutorial](https://tutorial.djangogirls.org/ja/)翻訳に参加
- アニメが好き（アイマス、ユーフォ）

+++

### アジェンダ

- 導入：Kaggleとは／タイタニックとは
- （ハンズオン）手を動かしてタイタニックコンペに参加
- 精度を上げるためのアプローチの紹介
- （もくもくタイム）精度向上に各自挑戦
- ハンズオン後のKaggle学び方案

---

### アジェンダ

- 導入：Kaggleとは／タイタニックとは
- （ハンズオン）手を動かしてタイタニックコンペに参加
- 精度を上げるためのアプローチの紹介
- （もくもくタイム）精度向上に各自挑戦
- ハンズオン後のKaggle学び方案

+++

### 導入

- Kaggleとは
- kaggleのコンペ
- タイタニックとは

+++

### Kaggleとは

- データサイエンスコンペのプラットフォーム
- 私のイメージ「機械学習を学ぶにはKaggleがいいらしい」
- 全世界で97000名超えが参加（2019/01/18 [アカウント数](https://www.kaggle.com/rankings)集計）
- 学習コンテンツ [Kaggle Learn](https://www.kaggle.com/learn/overview)

+++

### Kaggleのコンペ

2つのデータが与えられる

- 学習用データ
- テスト用データ

+++

### Kaggleのコンペ

- 学習用データから機械学習のモデルを構築
- モデルでテスト用データを推論し、その結果を提出
- 提出したデータのスコアが一番高い人（チーム）が優勝

+++

### タイタニックとは

- Kaggleの入門者用コンペ
- 沈没したタイタニック号の乗客データを扱う
- 教師あり学習 **分類** 問題：モデルは乗客の属性から、生存者／死亡者を予測する
- モデルの分類の精度(生存／死亡を正しく予想できた割合)を競う

+++

### 生存者／死亡者を予測

- モデルのイメージ＝推論
    - 28歳の男性がタイタニックに乗っていたら？ → 死亡
- モデルの構築：26歳の男性は死亡、30歳の男性は死亡、28歳の女性は生存、etc というデータがある

+++

### タイタニック号沈没事故

- Wikipedia [タイタニック号沈没事故](https://ja.m.wikipedia.org/wiki/%E3%82%BF%E3%82%A4%E3%82%BF%E3%83%8B%E3%83%83%E3%82%AF%E5%8F%B7%E6%B2%88%E6%B2%A1%E4%BA%8B%E6%95%85)
- 1912年4月の海難事故
- イギリス・サウサンプトンからアメリカ・ニューヨークへの航海中、氷山に衝突
- 2224人を乗せており、1513人が死亡

+++

## Are you ready?
##（アカウントはできましたか？）

---

### ハンズオン

ブラウザで2つの操作

1. KaggleでKernelを立ち上げる
2. サンプルコードのGistにアクセス
    - https://gist.github.com/ftnext/34d8ad1bacbd7b928915c12599af9f92
    - titanic_handson_sample_code.ipynb を使います

+++

https://www.kaggle.com/c/titanic

![Kernelをクリック](spz_Jan_titanic_handson/assets/2_go_titanic_kernel.png)

+++

![New Kernelをクリック](spz_Jan_titanic_handson/assets/3_go_new_kernel.png)

+++

![Notebookを選択](spz_Jan_titanic_handson/assets/4_choose_notebook.png)

+++

### データのサイズ確認

- 学習用データ：`train_df`
- テスト用データ：`test_df`
- `test_df`には、生存か死亡かを表すSurvived列がない（これを予測する）

+++

### 大まかな流れ

1. `train_df`からモデルを作る
    - 前処理（欠損値処理、カテゴリ変数の扱い）
    - 性能確認
2. 作成したモデルで`test_df`について予測する

+++

### タイタニック乗客データ

`train_df.info()`で確認

- 整数（int）
- 浮動小数点数（float）
- 文字列（object）

+++

### int

- PassengerId
- Pclass(チケットの等級)
- SibSp(同乗した兄弟/配偶者の人数)
- Parch(同乗した両親/子供の人数)
- Survived（0：死亡、1：生存）

+++

### float

- Age（推測があるため、浮動小数点数）
- Fare（運賃）

+++

### object

- Name
- Sex
- Ticket
- Cabin
- Embarked（乗船した港）

---

### 選択した特徴量について

- 生存／死亡を判断するのに使えそうな特徴量を選びたい
- **本来は可視化してから特徴量を選択** しますが、ここでは天下りです
- 可視化コードはGistの titanic_handson_visualization.ipynb 参照
- [特徴量の選択の参考になるkernelはこちら](https://www.kaggle.com/startupsci/titanic-data-science-solutions)

+++

### PclassとSurvived

![Pclass=1と3に注目](spz_Jan_titanic_handson/assets/5_pclass_count.png)

+++

### SexとSurvived

![男性と女性で生存率が大きく違う](spz_Jan_titanic_handson/assets/6_sex_count.png)

+++

### AgeとSurvived

![生存率が異なる年齢層がある](spz_Jan_titanic_handson/assets/7_age_count.png)

+++

### SibSpとSurvived

![SibSp=1に注目](spz_Jan_titanic_handson/assets/8_sibsp_count.png)

+++

### ParchとSurvived

![Parch=1と2に注目](spz_Jan_titanic_handson/assets/9_parch_count.png)

+++

### FareとSurvived

![死亡者が多い運賃の範囲がある](spz_Jan_titanic_handson/assets/10_fare_survived.png)

+++

### EmbarkedとSurvived

![Embarked=SとCに注目](spz_Jan_titanic_handson/assets/11_embarked_count.png)

---

### 欠損値

`train_df.isnull().sum()`, `test_df.isnull().sum()`で確認

- Age（20%程度）
- Fare（数件）
- Embarked（数件）
- Cabin（78%程度）

+++

### 欠損は何が問題か

- 欠損値（missing value）。欠測値とも呼ばれる
- データの収集過程で抜けてしまったなど
- 機械学習のツールは一般に欠損値に対処できない
- 削除すると貴重なデータが減るので、**埋める**

+++

### カテゴリ変数の数値化

- 文字列のラベルを値に持つ変数
    - Sex: male, female
    - Embarked: S, Q, C
- 文字列を整数に変換する

+++

### カテゴリ変数の数値化

- Sex: male=0, female=1として置き換え
- Embarked: ダミー変数化
    - S=1, Q=2, C=3とすると本来なかった大小関係が想定されてしまう
    - (S, Q, C)という形式で変数にする。例：Sは(1, 0, 0)となる

+++

### 使わないカラムの削除

- Name
- Ticket
- Cabin（欠損が多いため）
- PassengerIdも削除するが、後ほど行う

+++

### モデル作成のポイント

- `test_df`について予測する前に、どの程度の性能のモデルなのか確認したい
- そこで、`train_df`をランダムに2つに分ける（`train_test_split`）
    - `train_df`のうち7割でモデルを作る
    - 残りの3割でモデルの性能を評価する

+++

### モデル作成のポイント

- ランダムに分けているが、`random_state`引数の値が同じなら、**他の人が実行しても同じ** ようにランダムに分かれる
- 今回はすぐ提出するが、別のモデルを作ったときに、モデルの性能が芳しく無ければ提出しないと判断できる

+++

### 提出用データ

- 以下の形式のCSVとするように指定されている
- `test_df`に含まれるPassengerId 418件について行を作る

PassengerId | Survived
----- | -----
892 | 0
: | :
1309|1

+++

### 今回のスコア accuracy

- 418名のうち生死を正しく予想できたものの割合
- 1に近いほど性能がよい
- ref: https://www.kaggle.com/c/titanic#evaluation

+++

### 提出練習用データセット

- 試しに提出することができるデータセット
- 性能：0.76555
- ロジックはシンプル。女性が助かり、男性が死亡と予測

---

### 0.76555超えを目指す

- サンプルコードを組合せて見ましょう
- Ageの欠損の埋め方を見直す
- AgeとFareを数段階のカテゴリに変換する
- モデルのアルゴリズムを変える

+++

## もくもくタイムです！

+++

## 0.76555超えた人🙋

---

### まとめ

- 紹介したアルゴリズムについて補足
- さらなる工夫の紹介
- ハンズオン後の学び方案

+++

### 紹介したアルゴリズムについて

- LightGBMとXGBoostは学習を重ねすぎると精度が落ちていく
- 解決策：early_stopping

+++

### LightGBMでのearly_stopping

コード例を追加する

+++

### XGBoostでのearly_stopping

コード例を追加する

+++

### さらに工夫できる

- 年齢の小さいところで助かっている（4歳以下）Nameを加工してTitle
- 特徴量を作る
    - Aloneかどうか（SibSpとParchを加工する）
    - Pclass と Age（カテゴリ）の積
- 詳しくは[可視化の参考にしたkernel参照](https://www.kaggle.com/startupsci/titanic-data-science-solutions)

+++

### nikkieの考え

- データサイエンティストとエンジニアが協働できれば素敵
- 性能のいい機械学習モデルが作れなくても協働できる
    - 機械学習モデルをAPIにして他のアプリと連携
- クラウドベンダー公開の高性能な人工知能APIを使ってもいい
    - 例: Microsoft Cognitive Services

+++

### Follow your heart

- 機械学習体験、楽しかった😁
    - ハンズオンと同様のコードが書ける状態を目指してみては？
- 機械学習、意外とツライ。。😢
    - アプリケーションに人工知能APIを組み込むという視点で勉強してみては？

+++

### 参考書籍

- 『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』
    - ざっとつかめる。説明がわかりやすい
- 『Python機械学習プログラミング』（現在は[2版](https://www.amazon.co.jp/dp/4295003379)）
    - 機械学習の概念について詳細な説明

+++

### 充実のオンライン教材（これからやりたい）

- Kaggle Learn
- [Coursera Machine Learning](https://ja.coursera.org/lecture/machine-learning/what-is-machine-learning-Ujm7v)
- [Amazon　Machine Learning](https://aws.amazon.com/jp/training/learning-paths/machine-learning/)
- [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course/ml-intro)

+++

### （おまけ）タイタニック裏話

先のWikipediaを確認したところ・・・

- 救命ボートの数が全員分ない -> 女性と子供優先
- 客室係がさばく乗客の数が等級によって違う
- 三等船室からデッキまでたどり着けず（客室係と言葉が通じない問題）

+++

### ご清聴ありがとうございました
### ハンズオンお疲れさまでした！
Contact: [Twitter @ftnext](https://twitter.com/ftnext)
