# Amazon Machine Learningで機械学習始めませんか？
#### JAWS DAYS 2019 懇親会LT (2019/02/23) nikkie

---

## Do you know Amazon Machine Learning?

ご存知の方🙋

+++

### LT: Amazon MLで機械学習始めませんか？

- 対象：AWS経験あり・機械学習興味あり
- Amazon ML(Amazon Machine Learning)を紹介します
- @color[#316A5B](機械学習モデルの作成)と@color[#316A5B](アプリケーションへの組み込み)を話します

+++

### About nikkie

- 春から4年目、ソフトウェアエンジニア
- Love Python（Web開発、機械学習勉強中）
- Alias @ftnext でアウトプット：[Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- @color[#316A5B](AWS初学者、Amazon MLは業務で調査)

+++

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

---

### LT: Amazon MLで機械学習始めませんか？

1. @color[#316A5B](機械学習 in Amazon ML)
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

+++

### 機械学習とは

<span class="seventy-percent-img">
![データとアルゴリズムからモデル（推論のルール＝計算式）を作る](jaws_days_2019_amazonml/assets/201902jaws_lt.001.png)
</span>

+++

### Amazon MLにおける機械学習 1/3

<span class="seventy-percent-img">
![アルゴリズムはAmazon MLが用意、私たちはデータを用意](jaws_days_2019_amazonml/assets/201902jaws_lt.002.png)
</span>

+++

### Amazon MLにおける機械学習 2/3

- @color[#316A5B](知っているデータから知らないデータを予測)
- Amazon MLでは *教師あり学習* のみ可能

+++

### Amazon MLにおける機械学習 3/3

1. 知っているデータからAmazon MLで@color[#316A5B](モデル)を作る
2. @color[#316A5B](モデル)で知らないデータについて予測する

例としてタイタニック🛳️乗客データを用います

+++

### イメージ：乗客の生死予測

データ種別 | 年齢 | 性別 | 生死
----- | ----- | ----- | -----
知っているデータ | 26歳 | 男性 | 死亡
知っているデータ | 30歳 | 男性 | 死亡
知っているデータ | 28歳 | 女性 | 生存
@color[#316A5B](知らないデータ) | 28歳 | 男性 | @color[#316A5B](？(予測）)

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. @color[#316A5B](Amazon MLの特徴)
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

+++

### Amazon MLの特徴3点

1. ノンコーディングで機械学習
2. データはS3に用意
3. APIにして簡単にアプリ組み込み

+++

### 1.ノンコーディング＝ウィザード操作

<span class="eighty-percent-img">
![おなじみのウィザード操作で機械学習](jaws_days_2019_amazonml/assets/0_amazonml_wizard.png)
</span>

+++

### ウィザードの流れ

1. 手元のデータから@color[#316A5B](データソース)を作る
2. データソースから@color[#316A5B](MLモデル)を作る
3. MLモデルをAPIとしてデプロイする

+++

### 2.データはS3に用意

- @color[#316A5B](S3のファイルを指定)する
- Amazon MLが自動解析してデータソースを作る

+++

### 予測したい項目を指定するだけ

![乗客の生死を予測するように設定](jaws_days_2019_amazonml/assets/3_choose_target.png)

+++

### 3.MLモデルのデプロイ

![ウィザート操作でデプロイ可能](jaws_days_2019_amazonml/assets/6_deploy_mlmodel.png)

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. @color[#316A5B](機械学習モデルを組み込んだWebアプリ（デモ）)
4. まとめ

+++

### デモアプリ

- @color[#316A5B](「あなたがタイタニックに乗っていたら助かるでしょうか？」)
- AWS Lambdaにデプロイ
- 言語：Python
- フレームワーク：Flask

+++

### 機能1：フォーム入力から判定

<span class="seventy-percent-img">
![あなたの情報をフォームに入力するとタイタニック号で生き残るかどうか判定されます](jaws_days_2019_amazonml/assets/feature1_form.png)
</span>

+++

### 機能2：顔写真アップロードから判定

![フォーム入力の代わりに自撮りした顔写真をアップロードすることもできます](jaws_days_2019_amazonml/assets/feature2_upload.png)

+++

### デモアプリ構成図

<span class="seventy-percent-img">
![①顔写真をS3に配置、②S3のファイルを指定してRekognition呼び出し、③年齢と性別取得、④フォームからの入力情報と同じ形式にしてAmazon MLのAPI呼び出し、返ってきた結果を表示](jaws_days_2019_amazonml/assets/201902jaws_lt.003.png)
</span>

+++

# Demo

自撮りしてアップロードしてみます

![https://bit.ly/2VcfsKw](jaws_days_2019_amazonml/assets/demo_slide_QR.png)

+++

### 登壇者の方にご協力いただきました

図

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. @color[#316A5B](まとめ)

+++

### まとめ：Amazon MLでは

- @color[#316A5B](ノンコーディング)で機械学習モデルのAPIを作れる
- 機械学習に触れる@color[#316A5B](一歩目)となる
- @color[#316A5B](得意な言語からAPIを呼び出し)て、機械学習を既存のアプリに組み込みましょう

+++

### 機械学習の一歩目として

- ウィザードを通して@color[#316A5B](機械学習の考え方)に触れられる
- ウィザートの進め方、機械学習の考え方についてはAppendix参照（本LTも満漢全席）
- 考え方を掴んだら、コーディングで機械学習（in @color[#316A5B](SageMaker)）

+++?image=spz_Jan_titanic_handson/assets/6_sex_count.png&size=contain&opacity=40

### ネタバラシ

- データは女性や子供が助かりやすい傾向にある（男性の参加者の皆さん、ごめんなさい）
- 「女性と子供優先」ref: Wikipedia [タイタニック号沈没事故](https://ja.m.wikipedia.org/wiki/%E3%82%BF%E3%82%A4%E3%82%BF%E3%83%8B%E3%83%83%E3%82%AF%E5%8F%B7%E6%B2%88%E6%B2%A1%E4%BA%8B%E6%95%85)

+++

### Amazon MLで機械学習始めませんか？
### ご清聴ありがとうございました
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix

目次を入れる

+++

### 例：タイタニック乗客データ🛳️

年齢 | 性別 | チケット<br>クラス | 乗船港 | 生死
----- | ----- | ----- | ----- | -----
26歳 | 男性 | 2 | S | 死亡

- チケットクラスは上から1,2,3
- 乗船港は頭文字でS,Q,Cのいずれか

+++

### Amazon MLの用語

- データソース：機械学習に使うデータについてのデータ（例：Ageという項目は数値データ）
- MLモデル：Amazon MLで作ったモデル

+++

### (1)データソース作成

1. 手元のデータをS3にアップロード
2. 予測されたスキーマの確認
3. 予測したいデータの設定

+++

### (1-1)S3にアップロード

![CSVファイルをアップロード](jaws_days_2019_amazonml/assets/1_s3_bucket_upload.png)

+++

### (1-2)予測されたスキーマの確認

![Numericは数値、Categoricalは限られた数の文字列の値、Binaryは0または1](jaws_days_2019_amazonml/assets/2_confirm_schema.png)

+++

### (2)MLモデル作成

- S3にアップロードしたデータのうち、7割から
- 残りの3割でMLモデルの性能評価
- AUCは0.825（1に近いほど予測が正確）

+++

### デプロイ前に調整可能

![誤って生存と予測することが少なくなるように調整](jaws_days_2019_amazonml/assets/5_adjust_mlmodel.png)

+++

### MLモデルの性能評価

![データソースをランダムに分割し、一方でMLモデルを作り、残りでMLモデルを評価する](jaws_days_2019_amazonml/assets/4_random_split.png)

+++

### Amazon MLの流れ

図：S3にデータ→データソース→MLモデル→デプロイ（得意な言語からAPIとして呼び出す）

+++

### 機械学習の考え方（補足）

- 知っているデータから知らないデータを予測
- 知っているデータはモデル作成とモデル評価に分けて使う
- デプロイ前の調整
- [Amazon ML チュートリアル](https://docs.aws.amazon.com/ja_jp/machine-learning/latest/dg/tutorial.html)をやってみては？
