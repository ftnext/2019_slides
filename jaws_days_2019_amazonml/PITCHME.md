# Amazon Machine Learningで機械学習始めませんか？
#### JAWS DAYS 2019 懇親会LT (2019/02/23) nikkie

---

### LT: Amazon MLで機械学習始めませんか？

- Amazon ML(Amazon Machine Learning)を使った@color[#3A8687](機械学習モデルの作成)と@color[#3A8687](アプリケーションへの組み込み)を話します
- AWS経験豊富な皆さまの開発するアプリに、機械学習を組み込むきっかけになれば幸いです

+++

### About nikkie ([@ftnext](https://twitter.com/ftnext))

- 春から4年目、ソフトウェアエンジニア (Python@color[#eba3ff](@fa[heart]))
- 所属：[株式会社キカガク](https://www.kikagaku.co.jp/)（**当LTは個人の見解です**）
- @color[#3A8687](AWS初学者) 情報収集のために参加
- 業務で調査したAmazon MLを題材に@color[#3A8687](LT駆動開発)

+++

### LT: Amazon MLで機械学習始めませんか？

1. Amazon MLを使ったWebアプリ（デモ）
2. Amazon MLでの機械学習
3. まとめ

---

## Do you know Amazon Machine Learning?

ご存知の方🙋

+++

### 特徴1：ウィザード操作＝ノンコーディング

<span class="eighty-percent-img">
![おなじみのウィザード操作で機械学習](jaws_days_2019_amazonml/assets/0_amazonml_wizard.png)
</span>

+++

### 特徴2：機械学習の結果をAPIに

![ウィザート操作でデプロイ可能](jaws_days_2019_amazonml/assets/6_deploy_mlmodel.png)

+++

### Amazon MLを使ったWebアプリ (Can be Saved?)

- @color[#3A8687](「あなたがタイタニック号に乗っていたら助かるでしょうか？」)
- Amazon MLで乗客の属性（年齢・性別など）から生死を予測する@color[#3A8687](API)を構築
- デモアプリはAWS Lambdaにデプロイ（Python・Flask）

+++

### 機能1：フォーム入力✍️から助かるか判定

<span class="seventy-percent-img">
![あなたの情報をフォームに入力するとタイタニック号で生き残るかどうか判定されます](jaws_days_2019_amazonml/assets/feature1_form.png)
</span>

+++

### 機能1：フォーム入力✍️から助かるか判定

- 「28歳・男性がタイタニックに乗っていたら助かる？」
- フォームに「28歳・男性」と入力
- アプリはAPIに問い合わせて予測取得

+++

### 機能2：顔写真📸から助かるか判定

![フォーム入力の代わりに自撮りした顔写真をアップロードすることもできます](jaws_days_2019_amazonml/assets/feature2_upload.png)

+++

### 機能2：顔写真📸から助かるか判定

- Rekognitionで@color[#3A8687](顔写真から年齢と性別を推定)
- フォーム入力の場合と同様にAPIに問い合わせて予測取得

+++

# Demo

自撮り📸してアップロードしてみます

![https://bit.ly/2VcfsKw](jaws_days_2019_amazonml/assets/demo_slide_QR.png)

+++

### 前夜祭でご協力いただきました🙇‍ ‍

<span class="seventy-percent-img">
![海老原さん、佐々木さん、ありがとうございました](jaws_days_2019_amazonml/assets/201902jaws_lt.004.png)
</span>

+++

### デモアプリ構成図

<span class="seventy-percent-img">
![①顔写真をS3に配置、②S3のファイルを指定してRekognition呼び出し、③年齢と性別取得、④フォームからの入力情報と同じ形式にしてAmazon MLのAPI呼び出し、返ってきた結果を表示](jaws_days_2019_amazonml/assets/201902jaws_lt.003.png)
</span>

+++

### デモアプリ 注意事項

- 顔写真はS3に上がります（**懇親会後、責任を持って削除します**）
- 自分の顔を上げたくない方は@color[#3A8687](私を撮ってアップ)してみてください
- 些細な点でもフィードバックいただけると嬉しいです

---

### LT: Amazon MLで機械学習始めませんか？

1. Amazon MLを使ったWebアプリ（デモ）
2. @color[#3A8687](Amazon MLでの機械学習)
3. まとめ

+++

### 機械学習とは

<span class="seventy-percent-img">
![データとアルゴリズムからモデル（推論のルール＝計算式）を作る](jaws_days_2019_amazonml/assets/201902jaws_lt.001.png)
</span>

+++

### Amazon MLにおける機械学習

<span class="seventy-percent-img">
![アルゴリズムはAmazon MLが用意、私たちはデータをS3に用意](jaws_days_2019_amazonml/assets/201902jaws_lt.002.png)
</span>

+++

### 知っているデータから知らないデータを予測

1. 知っているデータからAmazon MLで@color[#3A8687](モデル)を作る
2. @color[#3A8687](モデル)で知らないデータについて予測する（モデルをAPIにして実現）

+++

### タイタニック🛳️乗客データ

データ種別 | 年齢 | 性別 | 生死
----- | ----- | ----- | -----
知っているデータ | 26歳 | 男性 | 死亡
知っているデータ | 30歳 | 男性 | 死亡
知っているデータ | 28歳 | 女性 | 生存
@color[#3A8687](知らないデータ) | 28歳 | 男性 | @color[#3A8687](？(予測）)

---

### LT: Amazon MLで機械学習始めませんか？

1. Amazon MLを使ったWebアプリ（デモ）
2. Amazon MLでの機械学習
3. @color[#3A8687](まとめ)

+++

### まとめ：Amazon MLは

- @color[#3A8687](ノンコーディング)で機械学習モデルのAPIを作れる
- @color[#3A8687](得意な言語からAPIを呼び出し)て、機械学習を既存のアプリに組み込みましょう
- Amazon MLのウィザードの詳細はAppendix参照（本LTも満漢全席😋）

+++

### Special Thanks 👏

- 海老原さん（[「講師と対戦」](https://jawsdays2019.jaws-ug.jp/session/2133/)チューター）
- 佐々木さん（[スタッフ・コアメンバー](https://jawsdays2019.jaws-ug.jp/staff/)）

+++

### Amazon MLでアプリに機械学習を組み込みませんか？
### ご清聴ありがとうございました
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix

- タイタニックデータとネタバラシ
- Amazon ML ウィザード全容
- ウィザードで触れた機械学習の考え方

+++

### 例：タイタニック乗客データ🛳️

年齢 | 性別 | チケット<br>クラス | 乗船港 | 生死
----- | ----- | ----- | ----- | -----
26歳 | 男性 | 2 | S | 死亡

- チケットクラスは上から1,2,3
- 乗船港は頭文字でS,Q,Cのいずれか

+++?image=spz_Jan_titanic_handson/assets/6_sex_count.png&size=contain&opacity=20

### ネタバラシ

- データは女性や子供が助かりやすい傾向にある（男性の参加者の皆さん、ごめんなさい）
- 「女性と子供優先」ref: Wikipedia [タイタニック号沈没事故](https://ja.m.wikipedia.org/wiki/%E3%82%BF%E3%82%A4%E3%82%BF%E3%83%8B%E3%83%83%E3%82%AF%E5%8F%B7%E6%B2%88%E6%B2%A1%E4%BA%8B%E6%95%85)

---

### ウィザードの流れ

1. 手元のデータから@color[#3A8687](データソース)を作る
2. データソースから@color[#3A8687](MLモデル)を作る
3. MLモデルをAPIとしてデプロイする

+++

### Amazon MLの用語

- データソース：機械学習に使うデータについてのデータ（例：Ageという項目は数値データ）
- MLモデル：Amazon MLで作ったモデル

---

### (1)データソース作成

1. 手元のデータをS3にアップロード
2. データソースを作るデータを指定
3. 予測したいデータの設定

+++

### (1-1)S3バケット作成

![Amazon MLと同じリージョンでバケットを作るのがオススメ（転送費用発生しない）](jaws_days_2019_amazonml/assets/appendix/1_s3_bucket.png)

+++

### (1-1)手元のデータをアップロード

![](jaws_days_2019_amazonml/assets/appendix/2_upload_csv.png)

+++

### S3にアップロードしました

![CSVファイルをアップロードしました](jaws_days_2019_amazonml/assets/1_s3_bucket_upload.png)

+++

### 以降は、Amazon ML側で操作

![machineで検索すると見つかります](jaws_days_2019_amazonml/assets/appendix/3_go_amazonml.png)

+++

### Amazon MLウィザード起動

![「Datasource and ML model」を選択](jaws_days_2019_amazonml/assets/appendix/4_select_wizard.png)

---

### (1-2)データソースを作るデータを指定

![S3のファイルを指定](jaws_days_2019_amazonml/assets/appendix/5_s3_file.png)

+++

### (1-2)読み取り許可を与えます

![読み取り許可を与えた後の状態](jaws_days_2019_amazonml/assets/appendix/6_s3_validation.png)

+++

### Amazon MLは自動でデータの型を推測

![Numericは数値、Categoricalは限られた数の文字列の値、Binaryは0または1](jaws_days_2019_amazonml/assets/2_confirm_schema.png)

+++

### (1-3)予測したいデータの設定

![乗客の生死を予測するように設定](jaws_days_2019_amazonml/assets/3_choose_target.png)

+++

![Row idはNoのままで進めます](jaws_days_2019_amazonml/assets/appendix/7_row_id.png)

+++

### データソース作成前の確認

![](jaws_days_2019_amazonml/assets/appendix/8_datasource_review.png)

+++

### (2)MLモデル作成

![引き続きMLモデル作成に移ります。Customを選択](jaws_days_2019_amazonml/assets/appendix/9_mlmodel_setting.png)

+++

![Recipeは変更しません](jaws_days_2019_amazonml/assets/appendix/10_recipe.png)

+++

![Advanced settingも変更しません](jaws_days_2019_amazonml/assets/appendix/11_advanced_setting.png)

+++

### ポイント：性能評価のための設定

![データソースをランダムに分割し、一方でMLモデルを作り、残りでMLモデルを評価する](jaws_days_2019_amazonml/assets/4_random_split.png)

+++

### MLモデル作成前の確認 1/2

![](jaws_days_2019_amazonml/assets/appendix/12_mlmodel_review.png)

+++

### MLモデル作成前の確認 2/2

![](jaws_days_2019_amazonml/assets/appendix/13_mlmodel_review2.png)

---

### (3)APIとしてデプロイ。その前に

- モデルの性能評価
  - S3にアップロードしたデータのうち、7割でモデル作成
  - 残りの3割でMLモデルの性能評価
- モデルの調整

+++

### モデルの性能評価(AUC)

予測の正確性を表す指標（1に近いほど正確）

![AUCは0.825](jaws_days_2019_amazonml/assets/appendix/14_mlmodel_auc.png)

+++

### モデルの予測の傾向を確認

![](jaws_days_2019_amazonml/assets/appendix/15_performance.png)

+++

### デプロイ前にモデルを調整

![誤って生存と予測することが少なくなるように調整](jaws_days_2019_amazonml/assets/5_adjust_mlmodel.png)

+++

### (3)「Create endpoint」の後の確認

![](jaws_days_2019_amazonml/assets/appendix/16_confirm_deploy.png)

+++

### (3)APIデプロイ完了です

![](jaws_days_2019_amazonml/assets/appendix/17_deployed.png)

---

### Amazon MLで機械学習の一歩目

- ウィザードを通して@color[#3A8687](機械学習の考え方)に触れられる
- 考え方を掴んだら、コーディングで機械学習（in @color[#3A8687](SageMaker)）

+++

### 機械学習の考え方

- 知っているデータから知らないデータを予測
- 知っているデータはモデル作成とモデル評価に分けて使う
- デプロイ前の調整
- [Amazon ML チュートリアル](https://docs.aws.amazon.com/ja_jp/machine-learning/latest/dg/tutorial.html)をやってみては？

+++

# EOF
