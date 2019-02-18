# Amazon Machine Learningで機械学習始めませんか？
#### JAWS DAYS 2019 懇親会LT (2019/02/23) nikkie

---

## Do you know Amazon Machine Learning?

ご存知の方🙋

+++

### LT: Amazon MLで機械学習始めませんか？

- 対象：AWS経験あり・機械学習興味あり
- Amazon ML(Amazon Machine Learning)を紹介します
- 機械学習モデルの作成とアプリケーションへの組み込みを話します

+++

### About nikkie

- 春から4年目、ソフトウェアエンジニア
- Love Python（Web開発、機械学習勉強中）
- Alias @ftnext でアウトプット：[Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- AWS初学者、Amazon MLは業務で調査

+++

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

+++

### 機械学習とは

<span class="seventy-percent-img">
![データとアルゴリズムからモデル（計算式の塊）を作る](spz_Jan_titanic_handson/assets/201901kaggel_talk.001.png)
</span>

+++

### Amazon MLにおける機械学習 1/3

図：アルゴリズムはAmazon MLが用意、私たちはデータを用意（機械学習とはの図を改変）

+++

### Amazon MLにおける機械学習 2/3

- 知っているデータから知らないデータを予測
- Amazon MLでは *教師あり学習* のみ可能

+++

### Amazon MLにおける機械学習 3/3

1. 知っているデータからAmazon MLでモデルを作る
2. モデルで知らないデータについて予測する

例としてタイタニック乗客データを用います

+++

### イメージ：乗客の生死予測

データ種別 | 年齢 | 性別 | 生死
----- | ----- | ----- | -----
知っているデータ | 26歳 | 男性 | 死亡
知っているデータ | 30歳 | 男性 | 死亡
知っているデータ | 28歳 | 女性 | 生存
知らないデータ | 28歳 | 男性 | ？(予測)

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

+++

### Amazon MLの特徴3点

1. ノンコーディングで機械学習
2. S3のデータを利用
3. APIにして簡単にアプリ組み込み

+++

### 1.ノンコーディング＝ウィザード操作

![おなじみのウィザード操作で機械学習](jaws_days_2019_amazonml/assets/0_amazonml_wizard.png)

+++

### ウィザードの流れ

1. 手元のデータから **データソース** を作る
2. データソースから **MLモデル** を作る
3. MLモデルをAPIとしてデプロイする

+++

### 2.S3のデータを利用

- 用意したデータ（ファイル）はS3に置く
- Amazon MLが自動解析してデータソースを作る
- 使うデータと、予測したい項目（ここでは生死）だけ指定する

+++

### 予測したいデータを設定

![乗客の生死を予測するように設定](jaws_days_2019_amazonml/assets/3_choose_target.png)

+++

### 3.MLモデルのデプロイ

![ウィザート操作でデプロイ可能](jaws_days_2019_amazonml/assets/6_deploy_mlmodel.png)

+++

### デプロイ前に調整可能

![誤って生存と予測することが少なくなるように調整](jaws_days_2019_amazonml/assets/5_adjust_mlmodel.png)

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

+++

### デモアプリ

- 「あなたがタイタニックに乗っていたら助かるでしょうか？」
- AWS Lambdaにデプロイ
- 言語：Python
- フレームワーク：Flask

+++

### デモアプリ構成図

図：構成書き出し、処理の流れ

+++

### 機能1：フォーム入力から判定

図：あなたの情報をフォームに入力するとタイタニック号で生き残るかどうか判定される（CSS適用後）

+++

### 機能2：顔写真アップロードから判定

図：フォーム入力の代わりに自撮りした顔写真をアップロードしてもよい（CSS適用後）

+++

顔写真の場合の構成図（Rekognition）

+++

# Demo

自撮りしてアップロードしてみます

QRコード

+++

### 登壇者の方にご協力いただきました

図

---

### LT: Amazon MLで機械学習始めませんか？

1. 機械学習 in Amazon ML
2. Amazon MLの特徴
3. 機械学習モデルを組み込んだWebアプリ（デモ）
4. まとめ

+++

### まとめ：Amazon MLでは

- ノンコーディングで機械学習モデルのAPIを作れる
- 得意な言語からAPIを呼び出して、機械学習を既存のアプリに組み込める
- ウィザードを進める中で機械学習の考え方に触れられる（一歩目に適する）

+++

### 機械学習の考え方

- 例1：知っているデータから知らないデータを予測
- 例2：デプロイ前の調整
- 考え方を掴んだら、コーディングで機械学習（in SageMaker）

+++

### ネタバラシ

- データは女性や子供が助かりやすい傾向にある（男性の参加者の皆さん、ごめんなさい）
- 「女性と子供優先」ref: Wikipedia [タイタニック号沈没事故](https://ja.m.wikipedia.org/wiki/%E3%82%BF%E3%82%A4%E3%82%BF%E3%83%8B%E3%83%83%E3%82%AF%E5%8F%B7%E6%B2%88%E6%B2%A1%E4%BA%8B%E6%95%85)

グラフ入れてもいいかも

+++

### Amazon MLで機械学習始めませんか？
### ご清聴ありがとうございました
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix

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

### MLモデルの性能評価

![データソースをランダムに分割し、一方でMLモデルを作り、残りでMLモデルを評価する](jaws_days_2019_amazonml/assets/4_random_split.png)

+++

### Amazon MLの流れ

図：S3にデータ→データソース→MLモデル→デプロイ（得意な言語からAPIとして呼び出す）

+++

### 機械学習の考え方（補足）

- 知っているデータはモデル作成とモデル評価に分けて使う
- [Amazon ML チュートリアル](https://docs.aws.amazon.com/ja_jp/machine-learning/latest/dg/tutorial.html)をやってみては？
