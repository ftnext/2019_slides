# QuoraコンペでKPT
#### キカガクもくもく会 (2019/02/10)

---

### このLTでは

- 1月に取り組んだ **Quoraコンペの振り返り** を共有します
- 注：勉強中の視点 & がっつり取り組んだわけではありません

+++

### 自己紹介

- キカガク所属のエンジニア
- 経験あり：Python × Web（Django、Flaskなど）
- 機械学習を勉強中（Kaggle）

+++

### お品書き：QuoraコンペでKPT

1. Quoraコンペとは
2. 振り返り（KPT）
3. 共有したいこと

---

### 1.Quoraコンペとは

- Kaggle
- Quoraコンペ

+++

### Kaggle

- データサイエンスコンペのプラットフォーム
- 私のイメージ「機械学習を学ぶにはKaggleがいいらしい」

+++

### Quoraコンペ 1/2

- [Quora Insincere Questions Classification](https://www.kaggle.com/c/quora-insincere-questions-classification)
- 2018/11〜2019/01 Kaggleで開催
- 自然言語処理（**2クラス分類**）

+++

### Quoraコンペ 2/2

- Quora（グローバル版Yahoo!知恵袋）がデータ（英語の質問文）を提供
- Insincere Questions（不誠実な質問。教師データの1%程度）を判定するモデルを作る
- **F1 Score** を競う

---

### 2.KPT

振り返りのフレームワーク

- Keep（よかったこと）
- Problem（うまくいかなかったこと）
- Try（うまくいかなかったことの修正・もっとよくする案）

+++

### Keep

- [評価されているKernel](https://www.kaggle.com/sudalairajkumar/a-look-at-different-embeddings)を写経するだけで学びがあった
- [Kerasのロイター通信データ（記事のカテゴリ分け）](http://cedro3.com/ai/keras-mlp-reuters/)が参考にできることに気づいた

後ほど共有します

+++

### Problem

- 時間を確保するのが難しい（Kernelを写経した後、自分で試す時間が取れず。。）
- （他の勉強会・アウトプットを優先したという事情もあります）

+++

### Try

- 評価されたKernel × チュートリアルでコードの書き換えに取り組む
- 2月は最終週に集中して[クジラコンペ（画像分類）](https://www.kaggle.com/c/humpback-whale-identification)に取り組む

---

### 3. 共有したいこと

- 進行状況を可視化するtqdm
- コンペ × サンプルデータ（チュートリアル）

+++

### tqdm

- 処理状況を可視化
- インストール：`pip install tqdm`
- コード例：`for i in tqdm(long_list)`

+++

![tqdmを使った例（Tokenizerでかかる時間が把握できた）](kikamoku_Feb_quora_kpt/assets/tqdm_image.png)

+++

### コンペ × サンプルデータ

- 先ほどのKernel（kerasのコード）写経後
- 「そこそこのスコアは出たが、どこを書き換えればいいかわからない🤨」
- → kerasのサンプルデータ`keras.datasets.reuters`

+++

### サンプルデータのチュートリアル記事

- 記事数が多い → 理解できるものが見つかる
- Tokenizer（文書のベクトル化）、max_words（上位何語からベクトル化するか）を知った
- 記事のコードを試そうとするも、今回は時間切れ（無念😖）

---

### まとめ：QuoraコンペでKPT

- QuoraコンペのKernelで知った **tqdmで進行状況可視化** が便利
- 次回は、Kernelの写経に加えて、サンプルデータの **チュートリアル記事をもとにKernelを書き換えて** みる

+++

### ご清聴ありがとうございました
### 機械学習の勉強お互い頑張りましょう💪
