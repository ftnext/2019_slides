### すかすかタイタニックハンズオン

- 導入：機械学習／Kaggle／タイタニック（10分）
- ハンズオン：手を動かしてタイタニックコンペに参加（35分）
- <div class="kaggle-color-highlight">まとめ（10分）</div>
- 質疑&もくもくタイム：精度向上に各自挑戦（20分程度）

+++

### まとめ

- ハンズオンの振り返り
- 機械学習の学び方案
- Kaggle取り組み方案

+++

### 再掲：機械学習の全体像

<span class="seventy-percent-img">
![問題設定→データ収集→分析→**前処理→モデル作成→モデル評価**→運用](spz_Jan_titanic_handson/assets/201901kaggel_talk.003.png)
</span>

+++

### 体験したこと

1. 分析（生存と関係するデータ項目を洗い出した）
2. 前処理（データは抜けや形式のために、そのままでは機械学習に持ち込めない）
3. モデル作成（わずか1行！）
4. モデル評価

---

### 機械学習の学び方案

1. 機械学習の考え方（欠損値やデータの分割など）
2. 実装できる状態（Pythonなど）
3. 理論（数学など）

+++

### 機械学習の考え方の一例

- 教師あり学習
  - 分類（タイタニックコンペが該当）
  - 回帰
- 教師なし学習

それぞれにおけるモデルの作り方や、性能評価の仕方など

+++

### 10月発売『[Kaggleで勝つデータ分析の技術](https://gihyo.jp/book/2019/978-4-297-10843-4)』

- 機械学習の考え方をみっちり学べそう（読んでいます）
- Kaggleについての詳細な説明あり

+++

### 『Kaggleで勝つ』が難しそうなら 1/2

『[Pythonによるあたらしいデータ分析の教科書](https://www.amazon.co.jp/dp/4798158348)』

- 2018/09刊。[資格試験](https://www.pythonic-exam.com/exam/analyist)のテキスト
- 機械学習の考え方、実装、理論までカバー

+++

### 『Kaggleで勝つ』が難しそうなら 2/2

『[東京大学のデータサイエンティスト育成講座](https://www.amazon.co.jp/dp/4839965250/)』

- 2019/03刊。東大の講座の書籍化
- 機械学習の考え方は深いところまで（バギング・ブースティングなど）。実装も

+++

### 実装できるようになりたければ

- Pythonを学ぶ：無料の[公式チュートリアル](https://docs.python.org/ja/3/tutorial/index.html)、有料のオンライン教材：[PyQ](https://pyq.jp/)など
- `pandas`や`scikit-learn`を深く学ぶ：『[pandasクックブック](https://www.amazon.co.jp/dp/425412242X)』、『[Pythonではじめる機械学習](https://www.amazon.co.jp/dp/4873117984/)』

+++

### ディープラーニングを学ぶ

- Kaggleのコンペでは、ディープラーニングを使うことも多い（知っているとNotebookが読める）
- ディープラーニングのパッケージ：TensorFlow, PyTorch, Chainer, ...
- 私は[TensorFlowチュートリアル](https://www.tensorflow.org/tutorials/)で学びました（機械学習の考え方も学べます）
- TODO：おすすめの本

---

### Kaggle取り組み方案

- 自分が興味をもてる開催中のコンペに参加。やりながら学べばいい
- 評価が高いKernel、スコアが高いKernelの写経からスタート
- 探す→まねる→工夫する で 順位上げに挑戦

+++

### Kernelを探す

https://www.kaggle.com/c/titanic/kernels

![投票数が多いもの、またはスコアが高いものに注目しましょう。また、言語で絞り込めます](spz_Mar_titanic_handson2/assets/titanic_kernels.png)

+++

### Kaggleをバリバリやっていきたい方へ

注：Kaggleをバリバリやっていない立場からの見解です

- 興味あるコンペのスコアを上げるために、必要なところだけつまみ食い学習
- Kagglerから情報入手（例 [カレーちゃん](https://twitter.com/currypurin)さんによる[チュートリアル](https://note.mu/currypurin/n/nf390914c721e)）
- 一番重要と思うのは、時間の確保（他は手を出せなくなる）