### すかすかタイタニックハンズオン

- <div class="kaggle-color-highlight">導入：機械学習／Kaggle／タイタニック（10分）</div>
- ハンズオン：手を動かしてタイタニックコンペに参加（35分）
- まとめ（10分）
- 質疑&もくもくタイム：精度向上に各自挑戦（10分）

+++

### 導入

1. 機械学習とは
2. Kaggleとは
3. タイタニックとは

---

@snap[north span-100]

### (1)機械学習とは

@snapend

@snap[east span-50 text-center]

@ul[](false)
- **データ** と **アルゴリズム** からモデルを作る
- アルゴリズムは計算方法（データからモデルを作る手順）
@ulend

@snapend

@snap[west span-50]

![図：データとアルゴリズムからモデルを作る](spz_Jan_titanic_handson/assets/201901kaggel_talk.001.png)

@snapend

+++

### モデル

- イメージ：**予測するためのルール**
- 実態は「計算式の塊」
- 人が決めるのではなく、データにアルゴリズムを適用して見出す

+++

### 機械学習の一例：知っているデータから知らないデータを予測

1. 知っているデータからモデルを作る
2. モデルで知らないデータについて予測する

このあと具体化します

+++

### 機械学習の流れ

<span class="seventy-percent-img">
![問題設定→データ収集→分析→前処理→モデル作成→モデル評価→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.002.png)
</span>

---

### (2)Kaggleとは

- データサイエンスコンペのプラットフォーム
- モデルの性能を競う
- 全世界で123000名超えが参加（2019/10/22 [アカウント数](https://www.kaggle.com/rankings)集計）

+++

### Kaggleの対象範囲

<span class="sixty-percent-img">
![問題設定→データ収集→**分析→前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.003.png)
</span>

今回体験していきます

+++

@snap[north span-100]

### Kaggleのコンペ 1/2

@snapend

@snap[east span-50 text-center]

@box[span-100](知っているデータから知らないデータを予測することが多い)

@ul[](false)
* モデル作成用データ（知っているデータ）
* 予測対象データ（知らないデータ）
@ulend

@snapend

@snap[west span-50]

![「モデル」を使って「知らないデータ」について予測する](spz_Jan_titanic_handson/assets/201901kaggel_talk.007.png)

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

- 乗客の属性と生存／死亡情報からモデルを作る
- 生存／死亡を知らない乗客について、モデルで生死を予測する（スコアとなる指標は、予測の正解率）
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
