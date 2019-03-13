# λ
## よく見たら片方楽してるアプリ開発
#### みんなのPython勉強会#43 (2019/03/13) nikkie

---

### LT: λ よく見たら片方楽してるアプリ開発

- 2019/02/23 JAWS DAYS 懇親会でLTしました
- 機械学習を使ったアプリケーションを@color[#DB8132](LT駆動開発)
- タイタニックの生存者予測アプリのデモ & 知ったことを共有

+++

### About nikkie

- Alias @ftnext: [Twitter](https://twitter.com/ftnext), [はてなブログ](http://nikkie-ftnext.hatenablog.com/)
- 2018/09〜 stapy 4代目LT王子
- 2019年はアウトプットに没頭していたら、春が来ました

+++

### 最近のアウトプット

- Django基礎ハンズオン（eLV勉強会）
  - part1：[2019/01/24](https://elv.connpass.com/event/114810/)、part2：[2019/02/14](https://elv.connpass.com/event/119181/)
- Kaggleタイタニックハンズオン（サポーターズ勉強会）
  - 第1回：[2019/01/30](https://supporterzcolab.com/event/677/)、第2回：[2019/03/05](https://supporterzcolab.com/event/740/)
  - @color[#DB8132](学生向けオンライン)勉強会 [2019/03/06](https://talent.supporterz.jp/events/2992699f-53ed-417b-abf7-7d7bba931037/) [2019/04/12](https://talent.supporterz.jp/events/d7384737-e2a6-4dc9-bc5e-f90e17e0924e/)

+++

### LT: λ よく見たら片方楽してるアプリ開発

- LT駆動開発したアプリの紹介
- LT駆動開発したアプリを支える技術
- まとめ

---

### LT: λ よく見たら片方楽してるアプリ開発

- @color[#DB8132](LT駆動開発したアプリの紹介)
- LT駆動開発したアプリを支える技術
- まとめ

+++

### アプリ：Can be saved?

あなたがタイタニック号に乗っていたら助かるでしょうか？

1. フォームの入力情報（年齢や性別）をもとに生存／死亡を予測
2. @color[#DB8132](顔写真)から年齢や性別を推測して、生存／死亡を予測

+++

### 顔写真から生存／死亡を判定

![あなたの顔写真をフォームからアップロードするとタイタニック号で生き残るかどうか判定されます](jaws_days_2019_amazonml/assets/feature2_upload.png)

+++

### 使ったAWSサービス 1/2

- Lambda：@color[#DB8132](ソースコードだけ用意)すればアプリケーションをデプロイできる（サーバレス）
- S3：ストレージ。アップロードされた顔写真を一時的に置く

+++

### 使ったAWSサービス 2/2

- Amazon Machine Learning：GUIで機械学習。タイタニックの@color[#DB8132](生存予測モデル)を作り@color[#DB8132](API化)
- Rekognition：AWSによる学習済みモデルのAPI。@color[#DB8132](顔写真から年齢と性別を推定)

+++

### 構成図

<span class="seventy-percent-img">
![①顔写真をS3に配置、②S3のファイルを指定してRekognition呼び出し、③年齢と性別取得、④フォームからの入力情報と同じ形式にしてAmazon MLのAPI呼び出し、返ってきた結果を表示](jaws_days_2019_amazonml/assets/201902jaws_lt.003.png)
</span>

+++

# Demo

自撮り📸してアップロードしてみます

![https://bit.ly/2VcfsKw](jaws_days_2019_amazonml/assets/demo_slide_QR.png)

+++

<span class="thirty-percent-img">
![私がタイタニックに乗っていたら、死亡してしまうそうです](stapy_Mar_easy_lambda/assets/titanic_app_image.jpg)
</span>

---

### LT: λ よく見たら片方楽してるアプリ開発

- LT駆動開発したアプリの紹介
- @color[#DB8132](LT駆動開発したアプリを支える技術)
- まとめ

+++

### Can be saved?を支える技術

2つのパッケージを紹介

- boto3
- zappa

+++

### Can be saved?を支える技術

2つのパッケージを紹介

- @color[#DB8132](boto3)
- zappa

+++

### boto3

- Python向けのSDK
- AWSのサービスをアプリ(Flask製)から呼び出す際に利用
- [ドキュメント](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)

+++

### Can be saved?でのboto3利用

1. 顔写真をS3にアップロード
2. S3の顔写真をRekognitionで推定
3. Amazon MLで作ったAPI呼び出し

Appendixも参照ください

+++

### boto3で顔写真をS3にアップロード

- フォームから送信された顔写真をS3（ストレージ）へ
- [S3.Client.upload_fileobj](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html#S3.Client.upload_fileobj)
- 注：顔写真は私のバケットに上がりますが、@color[#DB8132](責任持って中を見ずに消します)のでご安心ください

```python
s3 = boto3.client('s3')
# img_file: 開いたファイル
# BUCKET_NAME: アップロード先のバケット名
# key: ファイル名
s3.upload_fileobj(img_file, BUCKET_NAME, key)
```

+++

### アップロードされた顔写真のリンク取得も可能

- S3のファイルの期限付きリンク取得（imgタグに設定）
- [S3.Client.generate_presigned_url](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html#S3.Client.generate_presigned_url)

```python
img_url = s3.generate_presigned_url(
        'get_object',
        Params=params, # 辞書（バケット名、ファイル名）
        ExpiresIn=300
    )
```

---

### Can be saved?を支える技術

2つのパッケージを紹介

- boto3
- @color[#DB8132](zappa)

+++

### zappa

- @color[#DB8132](Lambdaへのデプロイを非常に簡単)にしてくれる
- 初回は`zappa init`→`zappa deploy dev`（devとして設定した場合）
- 以降は`zappa update dev`でソースコードの更新を反映
- 参考記事 [Zappaを使ってFlask appをAWS Lambda と API Gatewayにデプロイしてみた](https://dev.classmethod.jp/cloud/deploy-flask-app-aws-lambda-api-gateway-ja/)

+++

### zappaを使ってみて

- @color[#DB8132](ローカルで動けば、Lambdaにデプロイしても動く)
- それまで知っていたWebAppsと比べてだいぶ楽 参考：[WebAppsにデプロイは難しい (2018/05 stapy)](https://gitpitch.com/ftnext/2018_LTSlides/master?p=stapy_May_Flask_Azure)
- 裏で何をやっているのかは理解深めたい

---

### LT: λ よく見たら片方楽してるアプリ開発

- LT駆動開発したアプリの紹介
- LT駆動開発したアプリを支える技術
- @color[#DB8132](まとめ)

+++

### λ (AWS Lambda)

- λという字は、@color[#DB8132](短い棒に長い棒がもたれかかっている)
- 長い棒は@color[#DB8132](私たち開発者)（短い棒にもたれかかって楽をしている）

+++

### まとめ：λ よく見たら@color[#DB8132](私が楽してる)アプリ開発😆

- AWSでLT駆動開発して知ったことを共有
- @color[#DB8132](boto3)でAWSの各サービスが使い倒せる
- @color[#DB8132](zappa)はLambdaへのデプロイを非常に簡単にしてくれる
- これらを使い倒して楽していきましょう！

+++

### 関連情報

- [LT報告ブログ記事](https://nikkie-ftnext.hatenablog.com/entry/2019/02/24/093423)
- [ソースコードリポジトリ](https://github.com/ftnext/titanic-app-jaws2019)

+++

### ご清聴ありがとうございました
### 些細なことでもフィードバック大歓迎です
Contact: [Twitter @ftnext](https://twitter.com/ftnext)

---

### Appendix: boto3コード例

- S3の顔写真をRekognitionで推定
- Amazon MLで作ったAPI呼び出し

+++

### boto3でS3の画像をRekognitionで推定

- S3のファイル配置情報（バケット名+ファイル名）から呼び出せる
- [Rekognition.Client.detect_faces](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rekognition.html#Rekognition.Client.detect_faces)

```python
rek_client = boto3.client('rekognition')
response = rek_client.detect_faces(
        Image={
            'S3Object': {
                'Bucket': BUCKET_NAME,
                'Name': key
            }
        },
        Attributes=['ALL']
    )
```

+++

### boto3でAmazon MLのモデル呼び出し

- Amazon MLで用意したタイタニックの生存者予測モデルのAPIを呼び出す
- [MachineLearning.Client.predict](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/machinelearning.html#MachineLearning.Client.predict)

```python
client = boto3.client('machinelearning')
response = client.predict(
        MLModelId='モデルのID',
        Record=record, # モデルに渡すデータ(辞書)
        PredictEndpoint='https://realtime.machinelearning.us-east-1.amazonaws.com'
    )
```
